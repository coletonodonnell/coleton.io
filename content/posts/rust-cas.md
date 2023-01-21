---
author: "Coleton O'Donnell"
title: "A WIP CAS Written in Rust"
date: "2021-04-27"
description: "For my first Rust project, I decided to write a (semi-functioning) CAS in Rust. This is a casual overview of the code."
tags: ["rust", "programming"]
math: true
---

# Introduction
This project can be found [here on my GitHub.](https://github.com/coletonodonnell/rust-cas)

At FLVS we have a Coding Club which I am apart of. The club does a lot of things, but every once in a while we do club projects, where we work on something as a group or individually, then present the project. I had a lot of Ideas for this upcoming project, but as I was preparing for my ACT, specifically the Math section, I was quite annoyed that a CAS wasn't allowed on the test. In comparison, the SAT allows one of the math sections to have a calculator and it can be a CAS calculator. CAS stands for Computer Algebra System, a piece of software that can symbolically work with expressions. I love CAS a lot, not only because it helps me with my work but also I love the idea that I can symbolically work with expressions. Basically telling a computer how to work expressions. I had no idea how to write a CAS (and I still don't know how to write one well) but I decided that it'd be a fun idea to write one. I was reading the [*The Rust Programming Language*](https://doc.rust-lang.org/book/) by Steve Klabnik and Carol Nichols and was starting to get confident in the language, so I decided to challenge myself by writing a CAS. This CAS is written in sub par Rust code as this is only my first project in the language. This overview will assume you have a basic understanding of Rust.

# Knowledge Gathering
I first began by understanding what a CAS is composed of by parts, and most importantly what my implementation will be like. The resources for writing a CAS are quite minimal online, and I wasn't really in the mood to dig super deep into papers. Besides, I really wanted to create my own CAS without any sort of pre-written example code, and instead rely on an Abstract paper which goes over the *ideas* of a CAS vs. the *implementation* of a CAS. There is plenty of CAS libraries that I could have utilized to get an idea of how to write one, but I instead opted to just utilize parts of [The History of the Calculus and the Development of Computer Algebra Systems](http://www.math.wpi.edu/IQP/BVCalcHist/calc5.html#_Toc407004380), most notably Part 5 which goes over the ideas of a CAS. I haven't studied Calculus yet so it was a bit futile reading about stuff I don't fully understand yet.

The paper utilizes the idea of a "Syntax Tree" as the data structure to represent an equation. This is done so that there can be multiple variables and to further simplify expressions, but due to time constraints and just minimizing the complexity of the project I opted to use a Binary Tree instead, thus only allowing for one variable. The difference here is that the Syntax Tree can have more than two children node, while the Binary Tree can only have two. This implementation is far from ideal for actual usage, as basically any complex expression that would be worthwhile to compute would include more than one variable. Along with this, the CAS must work recursively. The CAS supports:

- Parenthesis
- Exponents
- Multiplication
- Division
- Addition
- Subtraction

{{< math.inline >}}
<p>
If that order sounds familiar it is because it is, it is PEMDAS, something everyone learns. The order of operations in this case must be weighted reverse though, SADMEP. In actuality though Division and Multiplication are waited the same, and so is Addition and Subtraction. So it more looks like ASMDEP, but we don't have subtraction so it finally is just AMDEP. Instead of looking for the left most expression, we would instead go for the right most. This is important because for an expression like \(x \div 3 \times 2\), if we worked it should be \(2 \times x \div 3\), but writing it as a tree and not using the ASMDEP right-left rule, it'd be like writing \(x \times (3 \div 2)\) and I don't think we want that. 
</p>
{{</ math.inline >}}


# What We Are Working With
## The Token Enum
The Token enum is defined as:
```rust
#[derive(Clone)]
pub enum Token {
    ADD,
    MUL,
    DIV,
    EXP,
    VAR(String),
    NUM(f32),
    LGROUP,
    RGROUP,
}
```
{{< math.inline >}}
<p>
These are what each node's `data_type` can be, but LGROUP and RGROUP end up never being on our tree. Subtraction can be removed as \(x - x\) can be defined as \(x + (-1 \times x)\) and \(-x\) can be defined as \(-1 \times x.\)
</p>
{{</ math.inline >}}

## The Tree Structure
The tree structure is defined as
```rust
#[derive(Clone)]
pub struct Node {
    data_type: token::Token,
    left: Option<Box<Node>>,
    right: Option<Box<Node>>,
}
```
The `Box` pointer puts data on the Heap. [This lecture by Sami Alqadi on the CS196 at Illinois channel](https://youtu.be/2q1AzGUwL7M) goes over Smart Pointers in the Context of a Linked Lists, which includes the `Box` pointer. If you want to understand these Smart Pointers more I recommend that video along with [Learn Rust With Entirely Too Many Linked Lists.](https://rust-unofficial.github.io/too-many-lists/index.html) Line 1 says that the Structure is cloneable. Each Node consists of 3 parts. One, a `data_type` that is a Token (as defined above). Two, an Option of a Box of a Node. And finally three, another Option of a Box of a Node. The left and right do matter, and the tree (should) follow these rules:
- When there are two NUMs, lesser NUM goes to the left.
- NUM Values always go to the left.
- VAR Values always go to the right unless there is another VAR or an Operator as sibling.
- Operators (which I refer to as Types in the comments) always go the right when there is NUM or VAR as sibling.

Exception:
EXP and DIV parents ignore these rules, as they are left vs. right child sensitive.

## Steps of the Program
1. Ask the user to input an expression.
2. Create a vector of `&str` objects, splitting them via the white spaces.
3. Convert the vector from `&str` to `String`.
4. Remove `\n` from the end of the expression if it exists.
5. Parse the Vector into `token::tokenize(string_vector)`.
6. Iterate over the vector and use `token::tokenizer` to tokenize each part of the Expression. `token::tokenize` splits up the expression into it's parts past what the vector did (eg. splitting `(3` into `(,3`.)
7. Return a Vector of `token::Token`.
8. Parse the Vector of `token::Token` into `tree::process(token_vector)`.
9. `tree::process(token_vector)` puts the vector into `token::fix_groups(token_vector)` which returns the fixed vector and all of the group locations. We will get into this process in a bit as this was actually one of the more fun things to work with.
10. Create a binary tree by calling the recursive function `tree::node_creation(raw_node)`. Where `raw_node` is a vector created by `tree::split_locator(token_vector, group_locations)`. This basically splits the expression into two halves. This splits the expression down and down while also following the tree's rules. After we reach the bottom, it just returns all the way up, giving us a full tree that obeys the rules of PEMDAS.
11. Parse our binary tree (Node object) to `tree::simplify_node(node)`.
12. 'tree::simplify_node' is a recursive method that again splits nodes then works back up. This is a little more complex as it also matches broader expressions to a certain depth. This method is a WIP right now, as it requires a lot of pattern matching and with that, time. A lot of expressions work, but a lot more don't.
13. Return the simplified node.
14. Once we have this node, we print it out. Down the line it'd be optimal to use a parser written by another Team Member that generates a picture of the tree.

# Algorithm Breakdown
I won't be going into everything I wrote for this, that would be too long. I will go over some stuff I enjoyed writing though. The comments on most of everything is good enough to learn what is going on with minimal knowledge of Rust, so if you want to take a look at it all and laugh at how I wrote some things, go ahead.

## `find_groups()`
I really enjoyed writing this one and I think I came up with a clever way of doing it. This function does as it says, it finds groups. This problem was one of the more fun ones to solve.

Full Implementation:
```rust
// Find groupings.
fn find_groups(token_vector: Vec<Token>) -> Vec<(i32, i32)> {
    let mut total_group: i32 = 0;

    // find total LGROUP and RGROUP
    for i in 0..token_vector.len() as i32 {
        match token_vector[i as usize] {
            Token::LGROUP => {
                total_group += 1;
            } Token::RGROUP => {
                total_group += 1;
            }
            _ => {}
        }
    }

    // If the total group is uneven, crash.
    if total_group % 2 != 0 {
        panic!("There must be an even number of group symbols!")
    }

    // Declare group_locations
    let mut group_locations: Vec<(i32, i32)> = Vec::new();

    // if there isn't any groups at all, just return the empty vector
    if total_group == 0 {
        return group_locations
    }

    // declare variables logic for the locating of parenthesis beginning and end locations
    let mut unsorted_lgroup_locations: Vec<i32> = Vec::new();
    let mut left_right_value: usize = 0;
    let mut right_right_value: usize = 0;

    // search for all left values before the first right
    for i in 0..token_vector.len() as i32 {
        match token_vector[i as usize] {
            Token::LGROUP => {
                unsorted_lgroup_locations.push(i);
            } Token::RGROUP => {
                left_right_value = i as usize;
                // if there is only one left value, push it and return group_locations
                if total_group / 2 == 1 {
                    group_locations.push((unsorted_lgroup_locations.pop().unwrap(), left_right_value as i32));
                    return group_locations
                }
                // break unless so as to search for the rest
                break;
            }
            _ => {}
        }
    }

    // Loop over until the group locations are empty
    while unsorted_lgroup_locations.is_empty() != true {
        // push right most left and known right
        group_locations.push((unsorted_lgroup_locations.pop().unwrap(), left_right_value as i32));

        // look for next right value between left and token_vector.len(), whilst also marking down left values
        for i in left_right_value as i32 + 1..token_vector.len() as i32 {
            match token_vector[i as usize] {
                Token::LGROUP => {
                    unsorted_lgroup_locations.push(i as i32);
                }
                Token::RGROUP => {
                    // if the right value in question isn't the last one we searched for, continue
                    if i != left_right_value as i32 {
                        // Set the new right value as right_right_value and break
                        right_right_value = i as usize;
                        break;
                    }
                }
                _ => {}
            }
        }
        // set left_right_value as the right_right_value, thus moving the block over.
        left_right_value = right_right_value;
    }

    // Declare variables for sorting.
    let mut sorted_group_locations: Vec<(i32, i32)> = Vec::new();
    sorted_group_locations.push((-1, -1));
    let mut next: (i32, i32);
    let mut insertion: i32;
    let mut k: i32;
    let mut copy: (i32, i32);

    // Sort the group_locations vector by left value small to large.
    for i in 0..group_locations.len() as i32 {
        next = group_locations[i as usize];
        insertion = 0;
        k = i;
        while k > 0 && insertion == 0 {
            if next.0 > sorted_group_locations[k as usize - 1].0 {
                insertion = k;
            } else {
                if k == sorted_group_locations.len() as i32 {
                    sorted_group_locations.push(sorted_group_locations[k as usize - 1]);
                } else {
                    copy = sorted_group_locations[(k as usize) - 1];
                    let _ = std::mem::replace(&mut sorted_group_locations[k as usize], copy);
                }
            }
            k -= 1;
        }
        if insertion == sorted_group_locations.len() as i32 {
            sorted_group_locations.push(next);
        } else {
            let _ = std::mem::replace(&mut sorted_group_locations[insertion as usize], next);
        }
    }
    return sorted_group_locations
}
```

- Lines 5-20: Find the total number of group values and if it isn't divisible by 2, crash. We can't have an uneven number of parenthesis, as that suggests they aren't matched. Technically this doesn't stop against ())) as that is still an even number but it is at least something.
- Lines 22-28: Declare `group_locations` as a Vector of `i32` tuples. Then, if the `total_group` is equal to 0, we just return an empty vector.
- Lines 30-52: We declare `unsorted_lgroup_locations`, `left_right_value` and `right_right_value` and then search for all left values until we find a right. Once we find a right, set the `left_right_value` to equal that place, and if there is only one pair of `LGROUP` and `RGROUP` values, push these locations to `group_locations` and return it, otherwise break.
- Lines 54-78: While our `unsorted_lgroup_locations` isn't empty, we are going to pop the last `lgroup` value in the Vector then push that value along with our `left_right_value`. After, we iterate from the `left_right_value + 1` and the `token_vector` length, thus shifting us over to find more left values then break if you find a right value. Repeat this process until we don't have any left values.
- Lines 80-113: Now that we have the locations, we need to sort the values via the `left_value` in each vector, small to large. This is done using a selection sort, and I won't get into that as that is pretty basic.

## `node_creation()`
The recursive `node_creation()` function is used to create a Node, and as a result, the entire tree. It utilizes a function called `split_locater()` to further split passed in branches. The `node_creation()` function relies on this heavily to further split the Nodes. 

Full Implementation:
```rust
// The actual creation of a node, including logic to determine left and right weighting.
fn node_creation(raw_node: (Vec<token::Token>, Vec<(i32, i32)>, Vec<token::Token>, Vec<(i32, i32)>, token::Token)) -> Option<Box<Node>> {
    let left_branch: Vec<token::Token> = raw_node.0;
    let left_group_locations: Vec<(i32, i32)> = raw_node.1;
    let right_branch: Vec<token::Token> = raw_node.2;
    let right_group_locations: Vec<(i32, i32)> = raw_node.3;
    let data_type_node: token::Token = raw_node.4;
    let a: Node;

    // If both of the branches are empty (eg. this is a VAR or NUM) just return this as a complete node (left and rights are empty.)
    if left_branch.is_empty() && right_branch.is_empty() {
        a = Node {
            data_type: data_type_node,
            left: None,
            right: None,
        };

    // If this isn't the case, we need to make sure we find what goes where, left vs. right. The weighting for this operation is as follows:
    // - If there are two NUM, lesser NUM goes to the left.
    // - If there is NUM and VAR, NUM goes to the left.
    // - If there is NUM and Operator (MUL, DIV, etc.), NUM goes to the left.
    // - If there is VAR and Operator (MUL, DIV, etc.), VAR goes to the left.
    // - SPECIAL CASE: If the data_type_node is EXP, then ignore all the above.
    // - SPECIAL CASE: If the data_type_node is DIV, then ignore all the above.
    } else {
        match data_type_node {
            token::Token::EXP => {
                a = Node {
                    data_type: data_type_node,
                    left: node_creation(split_locater(left_branch, left_group_locations)),
                    right: node_creation(split_locater(right_branch, right_group_locations)),
                };
                return Some(Box::new(a));
            }
            token::Token::DIV => {
                a = Node {
                    data_type: data_type_node,
                    left: node_creation(split_locater(left_branch, left_group_locations)),
                    right: node_creation(split_locater(right_branch, right_group_locations)),
                };
                return Some(Box::new(a));
            }
            _ => {}
        }

        // Declare all needed variables for this operation
        // Raw branches, haven't been determined if they are left and right yet, and recursive, thus the branches won't be worked on till' their value is known
        let first_branch_raw: Option<Box<Node>> = node_creation(split_locater(left_branch, left_group_locations));
        let second_branch_raw: Option<Box<Node>> = node_creation(split_locater(right_branch, right_group_locations));

        // left and right processed, taken from first and second branch but determined placement.
        let left_branch_processed: Option<Box<Node>>;
        let right_branch_processed: Option<Box<Node>>;

        // number and a bool to say if it exists or not, as well as an Option float. The option is neccesary for the decleration of the number, even if it exists or not.
        let first_num: Option<f32>;
        let first_num_bool: bool;
        let second_num: Option<f32>;
        let second_num_bool: bool;

        // if a variable is the data_type in either first or second branch.
        let first_variable: bool;
        let second_variable: bool;

        // Match first data_type
        match first_branch_raw.clone().unwrap().data_type {
            token::Token::NUM(a) => {
                first_num = Some(a);
                first_num_bool = true;
                first_variable = false;
            }
            token::Token::VAR(_) => {
                first_variable = true;
                first_num_bool = false;
                first_num = None;
            }
            _ => {
                first_variable = false;
                first_num_bool = false;
                first_num = None;
            }
        }

        // match second data_type
        match second_branch_raw.clone().unwrap().data_type {
            token::Token::NUM(a) => {
                second_num = Some(a);
                second_num_bool = true;
                second_variable = false;
            }
            token::Token::VAR(_) => {
                second_variable = true;
                second_num_bool = false;
                second_num = None;
            }
            _ => {
                second_variable = false;
                second_num_bool = false;
                second_num = None;
            }
        }

        // if NUM is valid for both first and second data_type
        if first_num_bool == true && second_num_bool == true {
            // if first NUM is less than or equal to second num
            if first_num.unwrap() <= second_num.unwrap() {
                left_branch_processed = first_branch_raw;
                right_branch_processed = second_branch_raw;
            // else, second NUM is less than first num
            } else {
                left_branch_processed = second_branch_raw;
                right_branch_processed = first_branch_raw;
            }
        // if NUM exists in only first
        } else if first_num_bool == true {
            left_branch_processed = first_branch_raw;
            right_branch_processed = second_branch_raw;
        // if NUM exists in only second
        } else if second_num_bool == true {
            left_branch_processed = second_branch_raw;
            right_branch_processed = first_branch_raw;
        // if VAR in both
        } else if first_variable == true && second_variable == true {
            left_branch_processed = first_branch_raw;
            right_branch_processed = second_branch_raw;
        // if VAR in only first
        } else if first_variable == true {
            left_branch_processed = first_branch_raw;
            right_branch_processed = second_branch_raw;
        // if VAR in only second
        } else if second_variable == true {
            left_branch_processed = second_branch_raw;
            right_branch_processed = first_branch_raw;
        // ABSTRACT in both
        } else {
            left_branch_processed = first_branch_raw;
            right_branch_processed = second_branch_raw;
        }
        // Declare the node
        a = Node {
            data_type: data_type_node,
            left: left_branch_processed,
            right: right_branch_processed,
        };

    }
    // Return the node
    return Some(Box::new(a))
}
```
- Lines 3-8: Get values for each of the `raw_node`.
- Lines 10-17: If the branches are empy, that means that we are dealing with a `VAR` or `NUM` value, so just declare `a` as that Node.
- Lines 25-44: Now that we have established we aren't working with `VAR` or `NUM`, we have to split this Node into left vs. right, but to do that we have to follow the rules as spoken about in Knowledge Gathering. In the case of Exponents or Division though, we can ignore these rules as they are left vs. right sensitive. So, we just declare `a` here if the `data_type` is `EXP` or `DIV`.
- Lines 46-54: Now that we have established we aren't working with `DIV` or `EXP` as our `data_type` we can now split the `first_branch_raw` as a `node_creation` of a split of the `left_branch` and it's `left_group_locations`. We do the same for `second_branch_raw`, just with the `right_branch`. We call these first and second as we don't know yet if the right will be on the left, or the left and right will just stay as left and right. We also declare the processed left and right branches, but they aren't being used right now.
- Lines 55-63: I did a little oopsie here and forgot that you can check None values in Rust, so there is some useless `bool` values here but it is fine, I will rewrite that part of the logic later.  These variables check if there is a `NUM` value for either left and right as well as `VAR` value for either left and right.
- Lines 65-101: Now, we determine if the `first_branch_raw` and `second_branch_raw` is composed of `NUM`, `VAR`, or neither. We do this using match statements. We store any `NUM` values so as to compare them later.
- Lines 103-138: This is a huge chain that basically finds left vs. right. The comments indicate what it is comparing. 
- Lines 140-148: Now that we have the `left_branch_process` and `right_branch_processed` values, we can declare that as `a` and then return `a`. When I rewrite this, I am going to remove the entire idea of `a` and instead just use `return` statements as it will be a bit faster.

# Conclusion
This was a really fun project, but it isn't quite finished yet. I still have to include more pattern matching and I would love to add one variable solving in the future. Coming from just learning Rust and knowing nothing about CAS, I am quite proud of how it turned out. Once I get some of the core features down, I plan on rewriting it to be a bit nicer and efficient, as well as turning it into a library instead of a program so you can import it. I hope that this project gives some insight into CAS at a very very basic level, as well as provides some good resources to learn more about them. I will update this later when I complete the project, either here or in a new article.

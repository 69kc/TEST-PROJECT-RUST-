# TEST-PROJECT-RUST-

*Implement a function that checks whether a given string is a palindrome or not.*

fn is_palindrome(string: &str) -> bool 
{
    let reversed = string.chars().rev().collect::<String>();
    string == reversed
}
fn main()
{
    let string1 = "malayalam";
    let string2 = "hello";
    
    println!("'{}' is a palindrome: {}", string1, is_palindrome(string1));
    println!("'{}' is a palindrome: {}", string2, is_palindrome(string2));
}
OUTPUT
'malayalam' is a palindrome: true
'hello' is a palindrome: false






*Given a string of words, implement a function that returns the shortest word in the string.*

fn shortest_word(string: &str) -> &str
{
    string.split_whitespace().min_by_key(|word| word.len(
    )).unwrap_or("")
}
fn main() 
{
    let string = "the quick brown fox jumps over the lazy dog";
    
    println!("The shortest word is: {}", shortest_word(string));
}
OUTPUT
The shortest word is: the







*Reverse a string in Rust*

fn reverse_string(string: &str) -> String
{
    string.chars().rev().collect()
}
fn main()
{
    let string = "Hello, world!";
    
    println!("The reversed string is: {}", reverse_string(string));
}
OUTPUT
The reversed string is: !dlrow ,olleH








*Check if a number is prime in Rust*

fn is_prime(number: u64) -> bool
{
    if number <= 1 {
        return false;
    }
    
    for i in 2..=((number as f64).sqrt() as u64) 
    {
        if number % i == 0 {
            return false;
        }
    }
    
    true
}
fn main()
{
    let number = 17;
    
    if is_prime(number) {
        println!("{} is prime", number);
    } else {
        println!("{} is not prime", number);
    }
}
OUTPUT
17 is prime










*Merge two sorted arrays in Rust*

fn merge_sorted_arrays(arr1: &[i32], arr2: &[i32]) -> Vec<i32>
{
    let mut merged_array = Vec::with_capacity(arr1.len() + arr2.len());
    let mut i = 0;
    let mut j = 0;
    
    while i < arr1.len() && j < arr2.len()
    {
        if arr1[i] < arr2[j] {
            merged_array.push(arr1[i]);
            i += 1;
        } else {
            merged_array.push(arr2[j]);
            j += 1;
        }
    }
    
    while i < arr1.len() 
    {
        merged_array.push(arr1[i]);
        i += 1;
    }
    
    while j < arr2.len()
    {
        merged_array.push(arr2[j]);
        j += 1;
    }
    
    merged_array
}
fn main() {
    let arr1 = [1, 3, 5, 7, 9];
    let arr2 = [2, 4, 6, 8, 10];
    
    let merged_array = merge_sorted_arrays(&arr1, &arr2);
    
    println!("{:?}", merged_array);
}
OUTPUT
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]









*Find the maximum subarray sum in Rust*


fn max_subarray_sum(arr: &[i32]) -> i32 {
    let mut max_so_far = 0;
    let mut max_ending_here = 0;
    
    for &num in arr {
        max_ending_here = i32::max(num, max_ending_here + num);
        max_so_far = i32::max(max_so_far, max_ending_here);
    }
    
    max_so_far
}
fn main() {
    let arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4];
    
    let max_sum = max_subarray_sum(&arr);
    
    println!("{}", max_sum);
}
 OUTPUT
 6



#Implement a function that checks whether a given number is prime or not.#

fn is_prime(n: i32) -> bool
{
    if n < 2 {
        return false;
    }
    
    for i in 2..=(n as f64).sqrt() as i32 {
        if n % i == 0 {
            return false;
        }
    }
    
    true
}
fn main()
{
    let num1 = 7;
    let num2 = 12;
    
    if is_prime(num1) 
    {
        println!("{} is prime", num1);
    } else {
        println!("{} is not prime", num1);
    }
    
    if is_prime(num2) 
    {
        println!("{} is prime", num2);
    } else {
        println!("{} is not prime", num2);
    }
}
OUTPUT
7 is prime
12 is not prime






*Implement a function that finds the longest common prefix of a given set of strings.*

fn longest_common_prefix(strs: &[String]) -> String {
    if strs.is_empty() {
        return String::new();
    }
    
    let first = &strs[0];
    let mut prefix = String::new();
    
    for (i, c) in first.char_indices() {
        for s in strs.iter().skip(1) {
            if i >= s.len() || s.chars().nth(i).unwrap() != c {
                return prefix;
            }
        }
        prefix.push(c);
    }
    
    prefix
}

fn main() {
    let strs1 = vec![String::from("flower"), String::from("flow"), String::from("flight")];
    let strs2 = vec![String::from("dog"), String::from("racecar"), String::from("car")];
    
    let prefix1 = longest_common_prefix(&strs1);
    let prefix2 = longest_common_prefix(&strs2);
    
    println!("{}", prefix1);
    println!("{}", prefix2);
}

OUTPUT
fl
""




*Given a binary tree, implement a function that returns the maximum depth of the tree.*



pub struct TreeNode {
    pub val: i32,
    pub left: Option<Rc<RefCell<TreeNode>>>,
    pub right: Option<Rc<RefCell<TreeNode>>>,
}

impl TreeNode {
    
    pub fn new(val: i32) -> Self {
        TreeNode {
            val,
            left: None,
            right: None,
        }
    }
}

use std::rc::Rc;
use std::cell::RefCell;

fn max_depth(root: Option<Rc<RefCell<TreeNode>>>) -> i32 {
    match root {
        Some(node) => {
            let left_depth = max_depth(node.borrow().left.clone());
            let right_depth = max_depth(node.borrow().right.clone());
            1 + left_depth.max(right_depth)
        },
        None => 0
    }
}

fn main() {
    let mut root = TreeNode::new(1);
    let mut node2 = TreeNode::new(2);
    let node3 = TreeNode::new(3);
    let node4 = TreeNode::new(4);
    let node5 = TreeNode::new(5);
    
    node2.left = Some(Rc::new(RefCell::new(node4)));
    node2.right = Some(Rc::new(RefCell::new(node5)));
    root.left = Some(Rc::new(RefCell::new(node2)));
    root.right = Some(Rc::new(RefCell::new(node3)));
    
    let depth = max_depth(Some(Rc::new(RefCell::new(root))));
    
    println!("{}", depth);
}
OUTPUT
3




*Given a sorted array of integers, implement a function that returns the median of the array.*

fn find_median_sorted_array(nums: &[i32]) -> f64
{
    let n = nums.len();
    if n % 2 == 0 {
        // If the array has even length, return the average of the middle two elements
        (nums[n / 2 - 1] + nums[n / 2]) as f64 / 2.0
    } else {
        // If the array has odd length, return the middle element
        nums[n / 2] as f64
    }
}
fn main()
{
    let nums = vec![1, 2, 3, 4, 5, 6];
    let median = find_median_sorted_array(&nums);
    println!("{}", median); // Output: 3.5
}
OUTPUT
3.5

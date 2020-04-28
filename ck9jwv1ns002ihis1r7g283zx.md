## Beautiful Matrix

Problem URL:  [Beautiful Matrix](https://codeforces.com/contest/263/problem/A)


> You've got a 5 × 5 matrix, consisting of 24 zeroes and a single number one. Let's index the matrix rows by numbers from 1 to 5 from top to bottom, let's index the matrix columns by numbers from 1 to 5 from left to right. In one move, you are allowed to apply one of the two following transformations to the matrix:

>Swap two neighboring matrix rows, that is, rows with indexes i and i + 1 for some integer i (1 ≤ i < 5).
Swap two neighboring matrix columns, that is, columns with indexes j and j + 1 for some integer j (1 ≤ j < 5).
You think that a matrix looks beautiful, if the single number one of the matrix is located in its middle (in the cell that is on the intersection of the third row and the third column). Count the minimum number of moves needed to make the matrix beautiful.

>Input
The input consists of five lines, each line contains five integers: the j-th integer in the i-th line of the input represents the element of the matrix that is located on the intersection of the i-th row and the j-th column. It is guaranteed that the matrix consists of 24 zeroes and a single number one.

>Output
Print a single integer — the minimum number of moves needed to make the matrix beautiful.

Here we need to identify the difference between the x,y of the 1's position with 3,3. Adding those absolute differences will give the minimum number of moves to make the matrix beautiful.


```
use std::io;

fn get_vec_of_numbers() -> Vec<u8> {
    let mut buffer = String::new();
    io::stdin().read_line(&mut buffer).expect("Failed to read from stdin");
    let numbers: Vec<u8> = buffer.trim().split(" ").map(|x| x.trim().parse::<u8>().expect("Not an integer")).collect();
    numbers
}

fn main(){
    let mut matrix: Vec<Vec<u8>> = Vec::new();
    let mut x_index_of_one: i32 = 6;
    let mut y_index_of_one: i32 = 6;
    for i in 0..5 {
        let row = get_vec_of_numbers();
        match row.iter().position(|&pos| pos == 1) {
            Some(pos) => {
                x_index_of_one = (pos+1) as i32;
                y_index_of_one = (i+1) as i32
            },
            None => {},
        }
        matrix.push(row);
    }
    println!("{}",((3-x_index_of_one).abs())+(3-y_index_of_one).abs());
}
``` 

 
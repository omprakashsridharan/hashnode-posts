## In Search of an Easy Problem

Problem URL:   [In Search of an Easy Problem](https://codeforces.com/problemset/problem/1030/A) 


```
use std::io;

fn get_vec_of_numbers() -> Vec<u32> {
    let mut buffer = String::new();
    io::stdin().read_line(&mut buffer).expect("Failed to read from stdin");
    let numbers: Vec<u32> = buffer.trim().split(" ").map(|x| x.trim().parse::<u32>().expect("Not an integer")).collect();
    numbers
}

fn main(){
    let mut number_of_people_buffer = String::new();
    io::stdin().read_line(&mut number_of_people_buffer).unwrap();
    let number_of_people: usize = number_of_people_buffer.trim().parse::<usize>().expect("Not an integer");
    let numbers = get_vec_of_numbers();
    let mut result = String::from("EASY");
    if numbers.len() != number_of_people {
        panic!("Number of inputs not same")
    }
    for i in numbers {
        if i == 1 {
            result = String::from("HARD");
            break;
        }
        continue;
    }
    print!("{}",result);
}
``` 


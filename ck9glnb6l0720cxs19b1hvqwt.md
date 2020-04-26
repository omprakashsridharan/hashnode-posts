## Bear and Big Brother

Problem URL:   [Bear and Big Brother](https://codeforces.com/problemset/problem/791/A) 

In this problem, we are give the weights of two bears ( Limbak and Bob ). Limbak wants to weigh heavier than Bob. Given their eating habits, Limbak tripples every year and Bob doubles every year. We need to find the number of full years that it takes for Limbak to be strictly heavier than Bob.


```
use std::io;

fn get_vec_of_numbers() -> Vec<u32> {
    let mut buffer = String::new();
    io::stdin().read_line(&mut buffer).expect("Failed to read from stdin");
    let numbers: Vec<u32> = buffer.trim().split(" ").map(|x| x.trim().parse::<u32>().expect("Not an integer")).collect();
    numbers
}

fn main() {
    let bear_weights: Vec<u32> = get_vec_of_numbers();
    let mut limbak_weight = bear_weights[0];
    let mut bob_weight = bear_weights[1];
    let mut number_of_years = 0;
    while limbak_weight <= bob_weight {
        number_of_years += 1;
        limbak_weight *= 3;
        bob_weight *= 2;
    } 
    print!("{}",number_of_years);
}
``` 

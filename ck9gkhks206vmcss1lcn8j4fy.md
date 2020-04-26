## Wrong Subtraction

Problem URL:  [Wrong Subtraction](https://codeforces.com/contest/977/problem/A) 

```
use std::io;

fn main(){
    let mut input_text = String::new();
    io::stdin().read_line(&mut input_text).expect("failed to read from stdin");
    let inputs: Vec<u32> = input_text.trim().split(" ").map(|x|{
         x.trim().parse().expect("Not an integer!")
    }).collect();
    let mut number = inputs[0];
    let mut times = inputs[1];

    while times > 0 {
        if number % 10 == 0 {
            number = number / 10;
        }else{
            number -= 1;
        }
        times -= 1;
    }
    print!("{}",number);
}
``` 

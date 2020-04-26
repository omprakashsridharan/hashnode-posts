## 705/A Hulk

Problem URL:  [Hulk](https://codeforces.com/problemset/problem/705/A) 


> Dr. Bruce Banner hates his enemies (like others don't). As we all know, he can barely talk when he turns into the incredible Hulk. That's why he asked you to help him to express his feelings. Hulk likes the Inception so much, and like that his feelings are complicated. They have n layers. The first layer is hate, second one is love, third one is hate and so on...For example if n = 1, then his feeling is "I hate it" or if n = 2 it's "I hate that I love it", and if n = 3 it's "I hate that I love that I hate it" and so on.

This problem could also be solved in a recursive fashion, but for the simplicity of understanding i have solved in iteratively.


```
use std::io;

fn get_single_number_from_stdin() -> u64 {
    let mut buffer = String::new();
    io::stdin().read_line(&mut buffer).unwrap();
    buffer.trim().parse::<u64>().expect("Not an integer")
}

fn main(){
    let inception_level = get_single_number_from_stdin();
    let mut result = String::new();
    let mut current_level = 1;
    while current_level <= inception_level {
        if current_level % 2 == 1 {
            result.push_str("I hate");
        }else{
            result.push_str("I love");
        }
        current_level += 1;
        if current_level > inception_level {
            break;
        }else{
            result.push_str(" that ");
        }
    }
    result.push_str(" it");
    print!("{}",result);
}
``` 

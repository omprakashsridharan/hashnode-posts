## Hit the lottery

Problem URL:  [Hit the lottery](https://codeforces.com/problemset/problem/996/A?csrf_token=a3f7b7d14092ebcea6d91cc36fef14f1) 

This problem uses a greedy approach.

```
use std::io;

fn get_single_number_from_stdin() -> u64 {
    let mut buffer = String::new();
    io::stdin().read_line(&mut buffer).unwrap();
    buffer.trim().parse::<u64>().expect("Not an integer")
}

fn main(){
    let mut dollars = get_single_number_from_stdin();
    let denominations = vec![100,20,10,5,1];
    let mut total_bills = 0;
    for denomination in denominations {
        if dollars == 0 {
            break;
        }
        if dollars >= denomination {
            let q = (dollars/denomination) as u64;
            dollars -= denomination * q;
            total_bills += q;
        }else{
            continue;
        }
    }
    print!("{}",total_bills);
}
``` 

Although for denominations that are not regular, the above algorithm will not give the least number of bills possible. We can use Dynamic Programming approach where we memorise the solution for the overlapping subproblems which drastically reduces the number of computations if the input is huge. Here is a version of the problem solved using dynamic programming.


```
use std::io;
use std::collections::HashMap;

fn get_single_number_from_stdin() -> usize {
    let mut buffer = String::new();
    io::stdin().read_line(&mut buffer).unwrap();
    buffer.trim().parse::<usize>().expect("Not an integer")
}

fn main(){
    let dollars = get_single_number_from_stdin();
    let denominations = vec![100,20,10,5,1];
    let mut result = HashMap::new();
    result.insert(0, 0);
    for i in 1..=dollars {
        for d in &denominations {
            if *d <= i {
                let sub_result = result.get(&(i - *d)).unwrap();
                if result.contains_key(sub_result) && sub_result + 1 < *result.get(&i).unwrap_or(&(std::i64::MAX as usize)) {
                    result.insert(i, sub_result + 1);
                }
            }
        }
        println!("amount {}",i);
    }
    println!("{}",result.get(&dollars).unwrap());
}
``` 


## Anton and Polyhedrons

Problem URL:  [Anton and Polyhedrons](https://codeforces.com/problemset/problem/785/A)

We are using the Rust's powerful match expression to compute the total_faces of given polyhedrons on the fly.


```
use std::io;

fn get_single_number_from_stdin() -> u64 {
    let mut buffer = String::new();
    io::stdin().read_line(&mut buffer).unwrap();
    buffer.trim().parse::<u64>().expect("Not an integer")
}

fn main(){
    let mut number_of_polyhedrons = get_single_number_from_stdin();
    let mut total_faces = 0;
    while number_of_polyhedrons > 0 {
        let mut buffer = String::new();
        io::stdin().read_line(&mut buffer).unwrap();
        total_faces += match buffer.to_ascii_lowercase().trim() {
            "tetrahedron" => 4,
            "cube" => 6,
            "octahedron" => 8,
            "dodecahedron" => 12,
            "icosahedron" => 20,
            _ => 0
        };
        number_of_polyhedrons -= 1;
    }
    println!("{}",total_faces);
}
``` 
 
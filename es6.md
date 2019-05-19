# Destructuring function arguments
we can destructure to pull/use args as local variables, assign defaults and give it better conventions
`function myFunc({someLongPropertyName: prop = 'Default string'} = {}) {
  console.log(prop);
}`
* inside the argument, we set a default value for object itself (to be an empty object) incase nothing gets passed in
  `{someLongPropertyName: prop = 'Default string'} = {}`
* we can rename our arguments to be used inside. So our argument that we pass to this function will be named "someLongPropertyName" and we will use "prop" within the function `someLongPropertyName: prop = 'Default string'`
* we assign default values for our function incase nothing is entered `someLongPropertyName: prop = 'Default string'`

### Destructure with Object.entries
```
let user = {
  name: "John",
  age: 30
};

// loop over keys-and-values
for (let [key, value] of Object.entries(user)) {
  alert(`${key}:${value}`); // name:John, then age:30
}
```

# Spread Rest params
we can look at the arguments as a strem of values or read them one at a time. Helps with currying.
```
function add(...args) {
    if (args.length < 3) {
        return add.bind(this, ...args);
    }
    return args[0] + args[1] + args[2];
    // const [x, y,z] = args;
    // return x + y + z;
}
```
add(1,2,4); // 7
add(1)(2)(4); // 7


```
let options = {
  title: "Menu",
  height: 200,
  width: 100
};

let {title, ...rest} = options;

// now title="Menu", rest={height: 200, width: 100}
alert(rest.height);  // 200
alert(rest.width);   // 100
```

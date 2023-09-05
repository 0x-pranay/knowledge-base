Ideas

- create a function which takes a reducer function and applies to both left and right sides
  - processBoth((data)=> data.row)
- create a function to access left and right values and modify
  - processOne('left', (data) => data )
  - processOne('right', (data)=> data)
- Display necessary functions in console.log output. 
-  Toggle auto compare
- Css improvements
- 

```
jdd.transform('both', obj => {
   return obj.rows.sort((a, b) => {
  const nameA = a.driverId;
  const nameB = b.driverId;

  if (nameA < nameB) {
    return -1;
  }
  if (nameA > nameB) {
    return 1;
  }
  return 0;
});
})
```


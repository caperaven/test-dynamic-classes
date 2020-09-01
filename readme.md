# CRS Collection Summary

## Introduction
This library creates a summary data object for fields in a object array.  
For string fields it groups unique values and counts how many times that value is used in the collection for that field.  
Number values get more summary values such as:

1. min
1. max
1. count
1. sum
1. ave
1. uniqueCount

uniqueCount indicates how many unique values for that field is in the collection.

## Usage

```js
// Step 1. get the data
const data = getData(100000);

// Step 2. create a processor function that will generate the summary
const processor = getFilterProcessor(data[0], ["code", "value", "isActive"]);

// Step 3. loop through the records you want to process and pass the record on to the processor for evaluation
for (let record of data) {
    processor.processRecord(record);
}

// Step 4. Once you have processed all the records, generate the summary object
const result = processor.getSummary();
```

You can reuse the processor as many times as you want.  
It is accepted that the fields you defined is actually in the objects that you are parsing on.  
The first parameter of getFilterProcessor is required.  
This object should represent the typical structure of the data including values that will indicate it's data type.
If you do not define the second parameter (what fields you want to process), it will create a summary for every field in that initial object.

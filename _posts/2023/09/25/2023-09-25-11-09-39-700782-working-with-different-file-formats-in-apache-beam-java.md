---
layout: post
title: "Working with different file formats in Apache Beam Java"
description: " "
date: 2023-09-25
tags: [ApacheBeam]
comments: true
share: true
---

## Working with JSON files

Handling JSON files is quite common in data processing workflows. Apache Beam Java makes it easy to parse and process JSON data using simple transformations. Here's an example of reading from a JSON file and extracting certain fields:

```java
PipelineOptions options = PipelineOptionsFactory.create();
Pipeline pipeline = Pipeline.create(options);

// Read from JSON file
PCollection<String> jsonLines = pipeline
        .apply(TextIO.read().from("data.json"));

// Parse JSON lines into objects
PCollection<MyCustomObject> objects = jsonLines.apply(ParDo.of(new DoFn<String, MyCustomObject>() {
    @ProcessElement
    public void processElement(ProcessContext c) {
        String jsonLine = c.element();
        // Parse JSON line into MyCustomObject
        MyCustomObject obj = parseJsonLineIntoObject(jsonLine);
        c.output(obj);
    }
}));
```

## Working with CSV files

Apache Beam Java provides convenient utilities to work with CSV files. You can easily read, write, and transform data in CSV format. Let's see an example of reading a CSV file and applying transformations:

```java
PipelineOptions options = PipelineOptionsFactory.create();
Pipeline pipeline = Pipeline.create(options);

// Read from CSV file
PCollection<String> csvLines = pipeline
        .apply(TextIO.read().from("data.csv"));

// Split CSV lines into fields
PCollection<List<String>> fields = csvLines
        .apply(ParDo.of(new DoFn<String, List<String>>() {
            @ProcessElement
            public void processElement(ProcessContext c) {
                String csvLine = c.element();
                // Split CSV line into fields
                List<String> fieldList = splitCsvLine(csvLine);
                c.output(fieldList);
            }
        }));

// Apply transformations on fields
PCollection<KV<String, Integer>> transformedFields = fields
        .apply(ParDo.of(new DoFn<List<String>, KV<String, Integer>>() {
            @ProcessElement
            public void processElement(ProcessContext c) {
                List<String> fieldList = c.element();
                // Transform fields and output
                String transformedField = transformFields(fieldList);
                c.output(KV.of(transformedField, 1));
            }
        }));
```

## Working with Avro files

Apache Beam Java also provides support for reading and writing Avro files. Avro is a popular data serialization system widely used in big data applications. Here's an example of reading from an Avro file and performing transformations:

```java
PipelineOptions options = PipelineOptionsFactory.create();
Pipeline pipeline = Pipeline.create(options);

// Read from Avro file
PCollection<GenericRecord> avroRecords = pipeline
    .apply(AvroIO.readGenericRecords(schema).from("data.avro"));

// Apply transformations on Avro records
PCollection<OutputRecord> transformedRecords = avroRecords
    .apply(ParDo.of(new DoFn<GenericRecord, OutputRecord>() {
        @ProcessElement
        public void processElement(ProcessContext c) {
            GenericRecord avroRecord = c.element();
            // Perform transformations on Avro record and output
            OutputRecord transformedRecord = transformRecord(avroRecord);
            c.output(transformedRecord);
        }
    }));
```

## Conclusion

Apache Beam Java provides a wide range of capabilities for working with different file formats in data processing workflows. Whether it's handling JSON, CSV, or Avro files, you can leverage the power of Apache Beam Java to read, write, and transform data efficiently. Start exploring the possibilities and simplify your data processing tasks!

#ApacheBeam #Java
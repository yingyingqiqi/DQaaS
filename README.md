##Data profiling and batch DQ assessmen

- `pyspark`: Pyspark code for the Data Quality Profiling and Data Quality Assessment;
- `dqrest`: resources and templates for the restful web service developed with flask;
- `data_demo`: 
    * `input.json`: input data example
    * `result.json`: output data example 
    * `assosciation_consistency.json`: example of an association rule that must be provided in order to compute the association consistency;
    * `config_file_example.txt`: example of a config file to run the on demand assessment; this file is generated by the rest service on a `POST` request;
    * `profiling_post_body.json`: example of the body of a `POST` request for a data profiling. The request must be authenticated with a token passed in the header `Authorization` field. The token is provided by the security module.
    * `assessment_post_body.json`: example of the body of a `POST` request for an on demand assessment. The request must be authenticated with a token passed in the header `Authorization` field. The token is provided by the security module.
- `screen`: screenshots of the web service dashboard.

The result folder, specified as a parameter in the `POST` request, produced by the profiling of two file ` <file_name_1> ` and ` <file_name_2> `  will have the following structure:

```
 <result_folder>
    │
    ├── extended_dataset
    │    ├──<file_name_1>
    │    │   └──part_file
    │    └──<file_name_2>
    │          └──part_file
    │
    └── other folder with aggregated dimensions
```

In the `extended_dataset` folder are stored the tuples extended with the following quality dimensions:

- `COMPLETENESS_MISSING`: non null attributes, over total attributes count.
- `ASSOCIATION_CONSISTENCY`: number of satisfied rules, over total rules count. Computed only if the user provides association consistency rules.
- `TIMELINESS_<timestamp_header>`: computed on all the attributes identified as timestamps, according to the timestamp format provided in the `POST` request.


The web service at `<IP_ADDRESS>:5000\get_all` provides a simple dashboard to check the status of the requests.  

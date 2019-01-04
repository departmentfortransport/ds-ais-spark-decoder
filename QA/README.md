# ds-ais/QA

To test that the decoder outputs the correct values we compare it against the outputs of an established AIS library, [libais](https://github.com/schwehr/libais). 

The general idea is to decode a sample of messages using `libais` output these to a `.csv` and then compare these results to that produced by the Scala decoder. So the unit tests in `/aisdecode/src/test` require the `.csv` files generated by `lib_ais_QA.py` to run. 

## Generating a verification dataset

1. Generate a sample of data to run the `python` decoder on. 
   ```sh
   head -n 1000000 original.dat > sample.dat
   ```

2. Set the environment variables in `./.envrc` to point at the location.

    *  `QA_CSV_PATH` refers to the directory that will contain the `.csv` files we are going to generate. The `python` programme will write the `.csv` out to the default path where the programme was initiated. 
    *  `QA_DAT_PATH` refers to the `.dat` sample created above. 

3. Run `lib_ais_QA.py`, this should generate the following files:   
    ```
    QA
    ├── 123.csv
    ├── 18.csv
    ├── 24_0.csv
    ├── 24_1.csv
    └──  5.csv
    ```

Once this is complete you can initiate the test suite using `sbt test` from the Scala projects root directory.
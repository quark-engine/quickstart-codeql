
# QuickStart CodeQL
In this tutorial, we will learn how to install and run CodeQL with an easy example.
We show how to detect CWE-798 in an Android application [ovaa](https://github.com/oversecured/ovaa).

### Step1: Install CodeQL

1. Download the CodeQL CLI bundle

```
$ wget https://github.com/github/codeql-action/releases/latest/download/codeql-bundle.tar.gz
$ tar -xvzf ./codeql-bundle.tar.gz
```

2. Adding `/<extraction-root>/codeql` to your PATH, so that you can run the executable as just CodeQL.


### Step2: Download the detection script

Clone CodeQL script repository by running:
```
$ git clone https://github.com/github/codeql.git
```
### Step3: Download the ovaa source code

Clone the ovaa source code repository by running:
```
$ git clone https://github.com/oversecured/ovaa.git
```

### Step4: Create CodeQL database

Create CodeQL ovaa database by running:
```
$ codeql database create ovaa-db/ -l=java -c='./gradlew --no-daemon clean assembleRelease' --overwrite
```

### Step5: Analyze the sample with CWE-798 script

- Analyzing ovaa with Codeql CWE-798 script.
```
$ codeql database analyze ovaa-db --format=csv --output=result.csv codeql/java/ql/src/Security/CWE/CWE-798/HardcodedCredentialsApiCall.ql
```

- You should now see the message in the terminal:
```
Running queries.
Did not find any ML models.
[1/1] No need to rerun codeql/java/ql/src/Security/CWE/CWE-798/HardcodedCredentialsApiCall.ql.
Shutting down query evaluator.
Interpreting results.
```

- The result will be saved in `result.csv`.


Here is the excerpt from `result.csv`. It shows where the CWE-798 occured.
![](https://i.imgur.com/2lWAXEN.png)



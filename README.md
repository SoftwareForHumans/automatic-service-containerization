# FEUP-DISS
All the materials developed during the development of my research "Automatic Service Containerization with Docker", which is the basis of my master thesis and of a scientific paper that will be published posteriorly.


## Instructions to replicate our study

1. Download the main repository and its subprojects with:

```bash
git clone --recurse-submodules git@github.com:Raidenkyu/automatic-service-containerization.git
```

2. change to the `hermit/` directory and run:
```bash
npm run install-hermit
```

3. change to the `dockerfile-diff/` directory and run:
```bash
npm run install-dockerfile-diff
```
    
4. To get a random project from GitHub, change to the `projects-fetcher/` directory and run:

```bash
npm start
```

If you receive an error saying that the limit of requests was execeed, please wait some minutes before retrying. If the operation succeeds you can find a project in the file `projects.csv`.
    
5. Navigate to the url of the project fetched in the previous step and clone the the respective project.
    
6. Change to the directory of the project and see if the original dockerfile of the project is too complex to hermit or not. Then rate the status of the project in the projects dataset as accepted or discarded. If the project was discarded, you don't need to follow the remaining steps.
    
7. Run hermit to generate the dockerfile with:

```bash
hermit -c -t <number of seconds to timeout>
```

Usually 10 seconds are enough.
    
8. Now you should have both the original "Dockerfile" and "Dockerfile.hermit". To compare them and evaluate hermit's dockerfile run:

```bash
dockerfile-diff Dockerfile Dockerfile.hermit
```

If evaluation process ended without problems then update the "generation" column in the file `projects.csv` with "successful". If not update with "failed-build", but if you think that by running some installation commands it will work update with "require-extra-steps". In the case of "failed-build" then you can ignore the following instructions.
    
9. To generate the file evaluations.csv the results collected by dockerfile-diff run:

```bash
dockerfile-diff print
```
    
10. Change to the `hermit-study/` directory and update the files `projects.csv` and `evaluations.csv` in the `res/` directory with the versions that resulted from this experiment.
    
11. Open `hermit.ipynb` in a Jupyter Notebook and analyse how the evaluations changed.

# Demo DVC

## Clone the git repository
```bash
git clone https://github.com/hmchuong/dvc-demo.git
```

## Create virtual environment
Create python3 environment
```bash
virtualenv -p python3 env
```
Activate environment
```bash
source ./env/bin/activate
```

## Set up DVC environment
### Install DVC
```bash
pip install dvc
```
### Init DVC
```bash
dvc init
```
### Add remote storage
To push to google cloud storage, firstly, you need to install Google Cloud SDK and add Google Cloud Credential
```bash
pip install google.cloud.storage
```
```bash
export GOOGLE_APPLICATION_CREDENTIALS=/Users/admin/projects/vietai-demo/dvc-demo/authen.json
```
Create a bucket on GCS and add to the dvc
```bash
dvc remote add -d gcs gs://vietai-test/dvc-demo
```
## Experiment
### Install Google Drive Downloader
```bash
pip install googledrivedownloader
```
### Clone the dataset and add to DVC
Download the dataset of assignment 3
```bash
python download_data.py
```
Add the data folder extracted to DVC
```bash
dvc add data
```
### Create a new version
```bash
git add -A
git commit -m "init dataset"
git tag 1.0
git push --tags origin master
dvc push
```
### Delete some files and make a new data version
We will remove the `sample_submission.csv` and make the new dataset version
```bash
rm data/sample_submission.csv
dvc add data
```
```bash
git add -A
git commit -m "remove submission file"
git tag 1.1
git push --tags origin master
dvc push
```

### Checkout versions
List out all versions
```bash
git for-each-ref --sort=-taggerdate --format '%(refname:short)' refs/tags
```
Checkout version 1.0
```bash
git checkout 1.0 && dvc pull && dvc checkout
```
You will see the file `sample_submission.csv` again

Checkout version 1.1
```bash
git checkout 1.1 && dvc pull && dvc checkout
```
The file `sample_submission.csv` disappears

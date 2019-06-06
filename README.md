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
pip install dvc==0.41.3
```
### Init DVC
```bash
dvc init
```
### Add remote storage
To push to google cloud storage, firstly, you need to add Google Cloud Credential
```bash
export GOOGLE_APPLICATION_CREDENTIALS=~/projects/vietai-demo/dvc-demo
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

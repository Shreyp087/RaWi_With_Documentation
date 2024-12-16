# Data-Driven Prototyping via Natural-Language-based GUI Retrieval

[![DOI](https://zenodo.org/badge/465262035.svg)](https://zenodo.org/badge/latestdoi/465262035)

The supplementary material of our submission to the ASE Journal is structured as follows:

- **data**: This directory contains all the datasets used for GUI ranking and all the materials and datasets from the conducted user study
- **gui2r**: This directory contains the overall Python-based implementation of the retrieval models and architecture from our paper
- **notebooks**: This directory contains several Jupyter Notebooks for (1) the creation of the GUI retrieval gold standard, (2) the style property extraction of GUI components, (3) the analysis of the user study and (4) the per-query analysis of the AQE evaluation results
- **webapp**: This directoy contains the prototypical implementation of our approach based on a Django web application


## Live Website Demo

[![Live Website Demo](https://img.shields.io/badge/Demo-Live-blue)](https://drive.google.com/file/d/1OuDit7PC7gTfMwUdiWyPOo9Lb2Yo7ghf/view?usp=sharing)


# RaWi Repository - Project Setup Guide

Welcome to the RaWi Repository setup guide. Follow the steps below to set up the project on your local machine.

---

## 1. Clone the Repository
Clone the repository using the following command:
```bash
git clone https://github.com/Shreyp087/RaWi_With_Documentation.git
```
Navigate to the cloned project directory:
```bash
cd RaWi_With_Documentation
```

---

## 2. Set Up a Virtual Environment
- Ensure **Python 3.10.10** is installed on your system.
- Create a virtual environment:
  ```bash
  python3 -m venv venv
  ```
- Activate the virtual environment:
  - On Linux/macOS:
    ```bash
    source venv/bin/activate
    ```
  - On Windows:
    ```bash
    venv\Scripts\activate
    ```
- or Can use:
    ```bash
    $env:PYTHONPATH = "$env:PYTHONPATH;PATH\to\RaWi_With_Documentation\gui2r"
    ```
---

## 3. Install Dependencies
Install the required dependencies from the `requirements.txt` file:
```bash
pip install -r requirements.txt
```

---

## 4. Set Up MySQL Database & SECRET KEY
1. Install MySQL if it is not already installed.
   mysql  Ver 9.0.1
  
- `pkg-config` must be installed on your system.
  - On Debian/Ubuntu: `sudo apt-get install pkg-config`
  - On macOS: `brew install pkg-config`
  - On Fedora: `sudo dnf install pkg-config`

3. Create a database named `gui2r`:
   ```sql
   CREATE DATABASE gui2r;
   ```
4. Update the database credentials in `settings.py` in webapp/gui2rapp/settings.py:
   - Set the appropriate database configurations.
   - Change `DEBUG = TRUE`.
  
5. Run the SECRET_KEY.py and paste the output of it into the SECRET_KEY="" in the webapp/gui2rapp/settings.py

---

## 5. Download and Set Up Resources
### a. Word2Vec Files
- Download Word2Vec files from [GitHub](https://github.com/tmikolov/word2vec).
- Extract and move the files to:
  - `/gui2r/gui2r/resources/`
  - `/webapp/gui2rapp/staticfiles/resources/`

### b. RICO Dataset
- Download the following files from [RICO Quick Downloads](http://www.interactionmining.org/rico.html#quick-downloads):
  - **UI Screenshots and View Hierarchies (6 GB)**
  - **UI Metadata (2 MB)**
  - **Play Store Metadata (2 MB)**
  - **UI Screenshots and Hierarchies with Semantic Annotations (150 MB)**
- Extract and move the files to:
  - `/gui2r/gui2r/resources/`
  - `/webapp/gui2rapp/staticfiles/resources/`

### c. BERT Model
- Download the BERT model from [here](https://storage.googleapis.com/bert_models/2020_02_20/uncased_L-12_H-768_A-12.zip).
- Extract and move the files to:
  - `/gui2r/gui2r/resources/`
  - `/webapp/gui2rapp/staticfiles/resources/`

### d. Word Embedding
- Download and install the word embedding from [Google Drive](https://drive.google.com/file/d/0B7XkCwpI5KDYNlNUTTlSS21pQmM/edit?usp=sharing).
- Create a directory named `embeddings` in the main directory and extract the file into `RaWi_With_Documentation/webapp/gui2r/resources/embeddings/GoogleNews-vectors-negative300.bin`
- Update the above `GoogleNews-vectors-negative300.bin` file path in the file `RaWi_With_Documentation/gui2r/gui2r/retrieval/ranker/bool_iwcs_ranker.py` in line 190 & 216


### e. Preproc_txt Directory
- Create a directory named `preproc_txt` in:
  ```bash
  /webapp/gui2rapp/staticfiles/resources/
  ```

### f. Nltk files
- Run python script nltk_download.py:
  ```bash
  python3 nltk_download.py
  ```

---

## 6. Check Django Configuration
Run the following command to verify the Django configuration located at `webapp/manage.py`:
```bash
python3 manage.py check
```
Install any missing modules or fix configuration issues as prompted.

---

## 7. Migration
1. Ensure your MySQL server is running.
2. Start the migration process using `manage.py` located at `webapp/manage.py`:
   ```bash
   python3 manage.py migrate
   ```
   - This step may take **3-4 hours** as it processes data from **72000 files** in the combined and semantic_annotations directories.
   - Running the model may take an additional **3 hours** (~1800 batches).

---

## 8. Test the Server
Run the test server with:
```bash
python3 manage.py testserver
```
- This will create a `test_gui2r` database in MySQL and test the Django configuration.

---

## 9. Run the Server
Start the Django server:
```bash
python3 manage.py runserver
```
- Tables will be created in the `gui2r` database in MySQL.
- The project will run on: [http://127.0.0.1:8000](http://127.0.0.1:8000).

---

## 10. Local Modifications for Data Fetching
### Adjust Fetch Locations
Replace the data-fetching URLs from: Note: Currently fetching URLs are updated in the code.Ignore this step
```
http://rawi-prototyping.com/static/resources/semantic_annotations/1.json
```
to:
```
http://127.0.0.1:8000/static/resources/semantic_annotations/1.json
```

### Server Down Issue
- The server fetching data from `http://rawi-prototyping.com/gui2r/v1/retrieval` is currently down.
- Fetch data locally and modify scripts accordingly.

### Manual Testing
- Manually added two image cards to the webpage for testing purposes.
- Attempt to retrieve data locally using the provided script.

---

Thank you for setting up the RaWi project. Feel free to report issues or contribute to the repository!

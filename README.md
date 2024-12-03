# RaWi Repository - Project Setup Guide

Welcome to the RaWi Repository setup guide. Follow the steps below to set up the project on your local machine.

---

## 1. Clone the Repository
Clone the repository using the following command:
```bash
git clone https://github.com/RaWi-Prototyping/RaWi
```
Navigate to the cloned project directory:
```bash
cd RaWi
```

---

## 2. Set Up a Virtual Environment
- Ensure **Python 3** is installed on your system.
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
    $env:PYTHONPATH = "$env:PYTHONPATH;PATH\to\Rawi\gui2r"
    ```
---

## 3. Install Dependencies
Install the required dependencies from the `requirements.txt` file:
```bash
pip install -r requirements.txt
```

---

## 4. Set Up MySQL Database
1. Install MySQL if it is not already installed.
2. Create a database named `gui2r`:
   ```sql
   CREATE DATABASE gui2r;
   ```
3. Update the database credentials in `settings.py`:
   - Set the appropriate database configurations.
   - Change `DEBUG = TRUE`.

---

## 5. Check Django Configuration
Run the following command to verify the Django configuration:
```bash
python3 manage.py check
```
Install any missing modules or fix configuration issues as prompted.

---

## 6. Download and Set Up Resources
### a. Word2Vec Files
- Download Word2Vec files from [GitHub](https://github.com/tmikolov/word2vec).
- Extract and move the files to:
  - `/gui2r/gui2r/resources/`
  - `/webapp/gui2rapp/static/resources/`

### b. RICO Dataset
- Download the following files from [RICO Quick Downloads](http://www.interactionmining.org/rico.html#quick-downloads):
  - **UI Screenshots and View Hierarchies (6 GB)**
  - **UI Metadata (2 MB)**
  - **Play Store Metadata (2 MB)**
  - **UI Screenshots and Hierarchies with Semantic Annotations (150 MB)**
- Extract and move the files to:
  - `/gui2r/gui2r/resources/`
  - `/webapp/gui2rapp/static/resources/`

### c. BERT Model
- Download the BERT model from [here](https://storage.googleapis.com/bert_models/2020_02_20/uncased_L-12_H-768_A-12.zip).
- Extract and move the files to:
  - `/gui2r/gui2r/resources/`
  - `/webapp/gui2rapp/static/resources/`

### d. Word Embedding
- Download and install the word embedding from [Google Drive](https://drive.google.com/file/d/0B7XkCwpI5KDYNlNUTTlSS21pQmM/edit?usp=sharing).
- Create a directory named `embeddings` in the main directory and extract the file into it.

### e. Preproc_txt Directory
- Create a directory named `preproc_txt` in:
  ```bash
  /webapp/gui2rapp/static/resources/
  ```

---

## 7. Migration
1. Ensure your MySQL server is running.
2. Start the migration process:
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
Replace the data-fetching URLs from:
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

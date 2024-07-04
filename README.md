# ChatIITK - An Advanced RAG ChatBot for IITK Junta 

Developed by BCS under its Summer Project - Lluminating Language

## Environment Setup 

The app is still in the prototyping stage, so before running, create a separate virtual environment to avoid conflicts.


```

conda create -n ChatIITK python=3.10.0
conda activate ChatIITK
```

After successfully creating a virtual environment, install all the requirements for the project:

```

pip install -r requirements.txt
```

## Inference 

Before starting inference, we need to ingest our data into our VectorDB (`ChromaDB` in this case).

You can change the device type to CPU or MPS if you don't have access to a GPU. By default, it will run on the best available compute (MPS or GPU); otherwise, it will use the CPU:

```

python ingest.py --device_type cuda
```
After the ingestion of data is complete, you can see local VectorDB files in the DB folder. Now: 
- To start the Terminal interface, `run python run_ChatIITK.py` 
  - Additional Flags with `run_ChatIITK.py`: 
    1. `--device_type cuda`(or `mps` or `cpu`): Select the compute on which you want to run the model.
 
    2. `--save_qa`: Store user questions and model responses into a CSV file. This file will be stored as `/local_chat_history/qa_log.csv`.
 
    3. `--use_history` or `-h: Enable chat history`. This is disabled by default. Enable it by using the `--use_history` or `-h flag`.
 
    4. `--show_sources`: Show which chunks are being retrieved from your retriever. By default, it will show 4 different sources/chunks. You can change the number of sources/chunks.
 
    5. `--help`: Get help on these flags.
 
- To start the Streamlit UI, run:

```

streamlit run ChatIITK_UI.py
```

## How to Select Different Embedding Models and LLM 
 
- To select different models, specify them in `constants.py`
 
- Change the `MODEL_ID` and `MODEL_BASENAME`. If you are using a quantized model (GGML, GPTQ, GGUF), you will need to provide `MODEL_BASENAME`. For unquantized models, set `MODEL_BASENAME` to `NONE`.
 
- Refer to the examples in the `constants.py` file and check the HuggingFace Hub for more models.

## Data Ingestion Process 
 
1. **Run the Ingestion Script** : Use the `ingest.py` script to ingest data into the `ChromaDB` vector database. This script processes raw data and stores it in a structured format, making it ready for retrieval during inference.
```

python ingest.py --device_type cuda
```
 
  - **Importance** : Ensures that the chatbot has access to the latest and most relevant data for accurate responses.
 
2. **Monitor the Ingestion Process** : The `file_ingest.log` file records details of the ingestion process, including any errors or warnings encountered. This helps in debugging and monitoring the ingestion process. 
  - **Importance** : Provides transparency and helps identify issues during data ingestion.

## Running the Chatbot 
 
1. **Terminal Interface** : To start the terminal interface, use:
```

python run_ChatIITK.py
```

Customize the behavior with various command-line flags for device type selection, enabling chat history, saving Q&A logs, and showing retrieved sources.
 
  - **Importance** : Offers a flexible way to interact with the chatbot using command-line options.
 
2. **Streamlit UI** : For a web interface, run:
```

streamlit run ChatIITK_UI.py
```
 
  - **Importance** : Provides a user-friendly graphical interface for interacting with the chatbot.

## Crawling and Data Extraction 
 
- **`crawl.py`** : This script is responsible for crawling and extracting data from specified sources. It gathers raw data that will be processed and ingested into the vector database. 
  - **Usage** : Automates the collection of data from various sources, ensuring the chatbot has diverse and comprehensive information.

## Managing Models 
 
- **`load_models.py`** : This file contains the code to load the necessary models, including embedding models and the large language models (LLMs). It ensures that the appropriate models are loaded into memory before running the chatbot. 
  - **Usage** : Facilitates the loading of different models based on requirements, improving the flexibility and performance of the chatbot.

## Using Prompt Templates 
 
- **`prompt_template_utils.py`** : This utility file provides functions for managing and utilizing prompt templates. It helps in formatting and structuring the prompts used to interact with the language models. 
  - **Usage** : Enhances the interaction quality by providing well-structured prompts, leading to better responses from the chatbot.

## Utility Functions 
 
- **`utils.py`** : This utility file includes various helper functions used throughout the project. These functions support tasks like data preprocessing, logging, and other common operations required by the chatbot. 
  - **Usage** : Offers reusable code snippets that streamline common tasks, improving the overall efficiency of the development process.

## Troubleshooting and Logs 
 
- **`file_ingest.log`** : Check this log file for any issues during the data ingestion process. 
  - **Importance** : Crucial for diagnosing and resolving problems during the ingestion phase.
 
- **General Debugging** : Use the logging and error messages to troubleshoot issues. Ensure that all required dependencies are installed and correctly configured. 
  - **Importance** : Helps maintain the stability and reliability of the chatbot by addressing errors promptly.

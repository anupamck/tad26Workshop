# RAG Testing Masterclass

Welcome to the repository for the workshop **"Build your own Retrieval Augmented Generation (RAG) model and qualify it with automated tests"** in Test Automation Days 2026.

This workshop is hands-on: you’ll run Jupyter Notebooks inside a Docker container. The notebooks contain Python code for building a RAG pipeline, calling an LLM, and evaluating results with LangSmith and Ragas.

This guide should help you get setup and running before the workshop starts. It should not take more than 30 minutes.

If you are stuck or have questions, please reach out to me at [ak@anukrit.de](mailto:ak@anukrit.de).


## Tools used

- **Docker** – Runs a consistent environment (Python, Jupyter, dependencies) in a container.
- **Jupyter Lab** – Browser-based notebooks for running Python interactively.
- **Python 3.13** – With packages from `requirements.txt`.
- **LangChain / LangGraph** – Framework for chains, agents, and RAG.
- **LangSmith** – Tracing and monitoring for LLM runs (optional but recommended).
- **OpenAI API** – LLM provider (e.g. GPT-4o-mini) used in the notebooks.
- **Ragas** – Evaluation metrics for RAG (faithfulness, answer relevance, etc.).

## Prerequisites

1. **Docker Desktop**  
   Download and install from [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop/).  
   Start Docker Desktop and ensure it’s running.

2. **LangSmith account and project**  
  Sign up at [smith.langchain.com](https://smith.langchain.com).  
  Create a project (e.g. `tad26-rag-workshop`) via the LangSmith UI (Tracing -> New Project).  
  Create an API key for tracing (Account -> Settings -> API Keys -> Personal Access Token).  
  You’ll add your project name and your API key to your environment file in the next step.  



## Environment file (`.env`)

In the file `.env` in the **root of this repository**, update the following values:
```
LANGSMITH_API_KEY=<YOUR_LANGSMITH_API_KEY>
LANGSMITH_PROJECT=<YOUR_LANGSMITH_PROJECT_NAME>
```
To get the value of `OPENAI_API_KEY`, head over to this [document](https://www.protectedtext.com/tad2026workshop) and use the password `tad2026`. Update the value of the `OPENAI_API_KEY`

## Start the environment and run the pre-flight notebook

1. Start Docker Desktop.

2. Run the following command to start the environment:
   ```bash
   docker compose up --build
   ```
   This will build the image and start the container. The first run may take about 2-3 minutes.

   When the container is ready, you should see a line like:

   ```text
    rag-workshop-jupyter  | [I 2026-02-08 16:33:58.550 ServerApp] Jupyter Server 2.17.0 is running at:
    rag-workshop-jupyter  | [I 2026-02-08 16:33:58.550 ServerApp] http://2867cf9e2cbf:8888/lab
    rag-workshop-jupyter  | [I 2026-02-08 16:33:58.550 ServerApp]     http://127.0.0.1:8888/lab
    ```
    Open the URL in your browser to access Jupyter Lab: http://localhost:8888/lab

3. **Run the pre-flight check**  
   - In Jupyter Lab UI, open the file `preFlightCheck.ipynb`.  
   - Follow the instructions in the notebook.  

4. **Stop the environment**  
   In the terminal where `docker compose up` is running, press **Ctrl+C**. 
   To start again later without rebuilding:
   ```bash
   docker compose up
   ```

5. **Verify tracing in LangSmith**
   - Open your LangSmith project and confirm you see the test run (Tracing -> `<your-project-name>`). 
   - You should see an execution trace for your pre-flight check.
This software needs to be run on Linux with Ollama installed 
This software requires Python 3.10.12 

with the dependencies mentioned in the req.txt file, This can be done using "pip install -r req.txt"

once you have installed the dependencies you can run the "Download courses.py", This will create a directory "HW courses" and will save all the preprocessed courses of Heriot-watt in the directory
Once the courses are downloaded, We can start the chat by running QA.py 

# Course Q&A Assistant using Embeddings + Local LLM

This project builds a local Question-Answer assistant that helps students explore course materials. The system loads course text files, identifies the most relevant content chunk based on a user query, and then optionally sends that chunk to a local LLM (via Ollama) for generating answers.

The system supports:

    Intelligent course selection
    
    Context-aware passage retrieval
    
    Stop-word removal + TF-IDF search
    
    Sentence-Transformer embeddings
    
    Local inference for privacy & speed

Core Features

    Component	Description
    Course recognition	Chooses the right course file based on query similarity
    Chunking	Splits course content using recursive text splitter
    Semantic search	Uses all-MiniLM-L6-V2 embeddings to match relevant context
    Refinement	TF-IDF + cosine similarity to pick most relevant passage
    Query preprocessing	Tokenization + stop-word filtering
    Answer generation	Optional: sends passage + query to local Ollama model
    Modes	Answer / Source / Answer+Source
    Interactive CLI	Fully conversational interface

System Behavior

    Interaction Flow
    
    User enters course-related query
    
    System selects closest matching course file
    
    File contents split into semantic passages
    
    Preprocess and vectorize query
    
    Find most relevant passage
    
    Optionally run passage through LLM
    
    Display answer and/or source link

Model & Libraries

Category	Library / Model
Embeddings	sentence-transformers/all-MiniLM-L6-V2
Text splitting	LangChain RecursiveCharacterTextSplitter
Similarity	TF-IDF + cosine similarity
NLTK	Tokenization + stopwords
Local inference	ollama run (optional)
Mode Controls
Command	Mode
/sys_a	Answer only
/sys_s	Source only
/sys_as	Answer + Source
/select_course	Switch to new course
/end	Exit
Folder Structure
/project
│── main.py
│── HW courses/
│    ├── course1.txt
│    ├── course2.txt
│    └── ...


Each course file should contain:

Course name: <name>
Course link: <URL>

<course content>
end of passage
<next passage>

How to Run
Prerequisites
pip install transformers langchain nltk scikit-learn torch


If using Ollama for responses:

ollama pull Cbot

Start the system
python main.py

Example Usage

User: “Tell me about MSc AI course”
System finds file with MSc AI content, locates relevant chunk, optionally queries Ollama, and prints answer + source.

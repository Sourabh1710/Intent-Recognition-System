
# Intent Recognition System Development

## Overview
Developing an efficient Intent Recognition System is crucial for enhancing user experience and ensuring seamless human-computer interactions. The goal of this project is to design and implement a system that accurately classifies user queries or commands into predefined categories or intents using Natural Language Processing (NLP) techniques. This system will enable applications to understand user intentions and respond appropriately, making interactions more intuitive and user-friendly.

## Dataset Overview
The dataset used for this project is structured in JSON format and contains various user intents along with their corresponding text examples and responses. Here is a detailed breakdown of the dataset:

- **Intents:** The dataset includes multiple predefined intents, such as "Greeting," "GreetingResponse," "CourtesyGreeting," "CourtesyGreetingResponse," "CurrentHumanQuery," "NameQuery," "RealNameQuery," "TimeQuery," and "Thanks."
- **Text Examples:** For each intent, there are several text examples that users might input. For instance, the "Greeting" intent includes text examples like "Hi," "Hello," and "Hola."
- **Responses:** Each intent is associated with a set of predefined responses that the system can use to reply to the user's input. For example, the "Greeting" intent has responses like "Hi human, please tell me your UnivIn user" and "Hello human, please tell me your UnivIn user."
- **Extensions:** Some intents include additional functionalities or extensions, such as updating user information or fetching current time.
- **Context Management:** The dataset also handles context management, where certain intents require maintaining or clearing the context for accurate response generation.

### Example Entries

#### Greeting Intent
- **Text Examples:** "Hi," "Hello," "Hola"
- **Responses:** "Hi human, please tell me your UnivIn user." "Hello, human, please tell me your UnivIn user."
- **Context:** Outgoing context set to "GreetingUserRequest"

#### GreetingResponse Intent
- **Text Examples:** "My user is Sourabh." "This is Sourabh."
- **Responses:** "Great! Hi <HUMAN>! How can I help?" "Good! Hi <HUMAN>, how can I help you?"
- **Context:** Incoming context "GreetingUserRequest" and clearing context after responding

#### TimeQuery Intent
- **Text Examples:** "What is the time?" "What's the time?"
- **Responses:** "One moment," "One sec."
- **Extension:** Fetches the current time and responds with "The time is %%TIME%%."

## Library Imports
The project utilizes several essential libraries, including:

- `numpy`: For numerical operations.
- `json`: For parsing and handling JSON formatted data.
- `re`: For working with regular expressions, useful for text processing.
- `tensorflow`: For building and training the machine learning models.
- `random`: For generating random numbers and performing random operations.
- `spacy`: For advanced Natural Language Processing tasks.

## Loading the NLP Model
The spaCy library is used to load a pre-trained English NLP model:
- **spaCy Model:** The `en_core_web_sm` model is a small English model that includes vocabulary, syntax, and named entities.

## Loading the Dataset
- **Opening the File:** The `with open('Intent.json') as f:` statement opens the `Intent.json` file in read mode.
- **Loading JSON Data:** The `json.load(f)` function parses the JSON data and converts it into a Python dictionary.

## Text Preprocessing
- **Function Definition:** The `preprocessing` function takes a string as input and cleans the text by removing unwanted characters and normalizing spaces.
- **Return Cleaned Text:** The cleaned and normalized text is returned.

## Data Preparation
- **Initialization:** Empty lists `inputs` and `targets` store preprocessed text examples and their corresponding intents. The `classes` list stores unique intent classes, and the `intent_doc` dictionary maps each intent to its list of responses.
- **Iterate Over Intents:** The code iterates over each intent in the dataset, preprocessing text examples and storing responses.

## Tokenization and Padding
- **Function Definition:** The `tokenize_data` function tokenizes and pads input text data.
- **Return Tokenizer and Sequences:** The function returns the tokenizer and the padded input sequences.

## Preprocessing Input Data
- **Tokenize and Pad Inputs:** The `tokenize_data` function is called with `inputs` to obtain the tokenizer and padded input sequences.

## Categorical Target Creation
- **Function Definition:** The `create_categorical_target` function converts target labels into a one-hot encoded tensor.
- **Return Categorical Tensor and Mapping:** The function returns the one-hot encoded tensor and the mapping from categorical indices to original target labels.

## Model Training Parameters
- **Epochs:** Number of training epochs.
- **Vocabulary Size:** Size of the vocabulary for tokenized data.
- **Embedding Dimension:** Dimensionality of the embedding space.
- **Model Units:** Number of units or neurons in the model layers.
- **Target Length:** Length of sequences in the target tensor.

## Model Architecture Definition
- **Embedding Layer:** Maps input sequences into a dense vector representation.
- **Bidirectional LSTM Layer:** Processes input sequences in both forward and backward directions with dropout for regularization.
- **Dense Layers:** Fully connected neural network layers with ReLU activation.
- **Dropout Layer:** Helps prevent overfitting.
- **Output Layer:** Uses softmax activation to output probabilities for each class.
- **Optimizer and Compilation:** Compiled with the Adam optimizer and categorical crossentropy loss function.
- **Model Summary:** Prints a summary of the model architecture.

## Model Training with Early Stopping
- **Early Stopping Callback:** Monitors training loss and stops training after 4 epochs without improvement.
- **Model Training:** Trains the model using the input and target tensors.

## Intent Recognition Response Function
- **Response Selection:** Selects a response based on the predicted category.
- **Function Definition:** Processes the input sentence, predicts the category, and selects a response.

## Interactive Chat Loop
- **User Input:** Prompts the user to input a message.
- **Quit Option:** Ends the chat session if the user inputs 'quit'.
- **Response Generation:** Generates and displays a response for other inputs.
- **Loop Continuation:** Continues to prompt for user input until 'quit' is entered.

## Conclusion
This project involves the development of an intent recognition system using NLP techniques, providing a seamless and intuitive user experience. The dataset, preprocessing steps, model architecture, training process, and interactive chat loop are all essential components contributing to the effectiveness of the system.

## Instructions for Running the Code
1. **Install Dependencies:**
   ```bash
   pip install numpy tensorflow spacy
   python -m spacy download en_core_web_sm 
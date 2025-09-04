🛒 Shopping List → Recipe Generator (Flan-T5)
📌 Project Overview

This project uses the Flan-T5 model from Hugging Face to generate recipe ideas from a given shopping list.
It is a text-to-text generation mini-project in Generative AI.

Input: A shopping list or paragraph containing ingredients.

Output: Creative recipe names with short descriptions.

Example:

Input: tomatoes, pasta, cheese, chicken
Output:
1. Cheesy Chicken Pasta Bake – Pasta baked with tomato sauce, chicken, and cheese.  
2. Grilled Chicken Spaghetti – Spaghetti in fresh tomato sauce topped with grilled chicken.  
3. Creamy Tomato Chicken Lasagna – Layers of pasta, chicken, cheese, and tomato cream sauce.  

🛠️ Tech Stack

Python

Hugging Face Transformers

Flan-T5 (google/flan-t5-small or google/flan-t5-base)

(Optional) Streamlit – for a simple web UI

🚀 Installation

Clone this repo (or copy the code files):

git clone https://github.com/your-username/recipe-generator.git
cd recipe-generator


Install dependencies:

pip install transformers sentencepiece streamlit


Run the Python script:

python recipe_generator.py


(Optional) Run the Streamlit app:

streamlit run app.py

📄 Usage
Python Script
from transformers import AutoTokenizer, AutoModelForSeq2SeqLM

model_name = "google/flan-t5-base"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForSeq2SeqLM.from_pretrained(model_name)

def generate_recipe(shopping_list):
    prompt = (
        f"You are a professional chef. Suggest 3 creative recipes using these ingredients: {shopping_list}. "
        "Each recipe should include a dish name and a short description."
    )
    inputs = tokenizer(prompt, return_tensors="pt", max_length=512, truncation=True)
    outputs = model.generate(**inputs, max_length=220, num_beams=5, no_repeat_ngram_size=2, early_stopping=True)
    return tokenizer.decode(outputs[0], skip_special_tokens=True)

print(generate_recipe("bread, butter, milk, honey"))

Streamlit App (Optional UI)
import streamlit as st

st.title("🛒 Shopping List → Recipe Generator")

user_input = st.text_area("Enter your shopping list:")

if st.button("Generate Recipes"):
    if user_input.strip():
        recipes = generate_recipe(user_input)
        st.write("### 🍴 Suggested Recipes:")
        st.write(recipes)
    else:
        st.warning("Please enter some ingredients!")

📊 Features

✅ Generates multiple recipe ideas from ingredients
✅ Works with simple lists or full paragraphs with scattered ingredients
✅ Can be extended with recipe categories (breakfast, dinner, dessert, etc.)
✅ Optional web app with Streamlit for easy testing

🔮 Future Improvements

Fine-tune the model on real recipe datasets

Add cuisine-specific outputs (Indian, Italian, Vegan, etc.)

Generate detailed step-by-step cooking instructions

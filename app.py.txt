import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt

st.title("Talking Rabbitt 🐰")
st.write("Conversational analytics demo")

uploaded_file = st.file_uploader("Upload CSV", type="csv")

if uploaded_file:
    df = pd.read_csv(uploaded_file)

    st.write(df)

    question = st.text_input("Ask a question about the data")

    if "highest revenue" in question.lower():
        region = df.groupby("Region")["Revenue"].sum().idxmax()
        st.success(f"{region} has highest revenue")

        chart = df.groupby("Region")["Revenue"].sum()

        fig, ax = plt.subplots()
        chart.plot(kind="bar", ax=ax)

        st.pyplot(fig)
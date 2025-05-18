import streamlit as st
import pandas as pd
import time
import random
from datetime import datetime

st.set_page_config(page_title="Aviator Multiplicador Preditor", layout="wide")

# Layout de título
st.markdown("<h1 style='text-align: center; color: red;'>✈️ Aviator Multiplicador Preditor</h1>", unsafe_allow_html=True)
st.image("images/logo.png", use_column_width=True)

# Simulando histórico de entradas
if "historico" not in st.session_state:
    st.session_state.historico = [round(random.uniform(1.0, 50.0), 2) for _ in range(50)]

# Função para previsão com IA (simulada)
def prever_multiplicador(historico):
    média = sum(historico[-10:]) / 10
    if média > 10:
        return random.uniform(1.0, 3.0), "🔴 Baixa"
    elif média > 3:
        return random.uniform(3.1, 9.9), "🟡 Média"
    else:
        return random.uniform(10.0, 50.0), "🟢 Alta"

# Gráfico histórico
st.subheader("📊 Histórico de Últimos Multiplicadores")
df = pd.DataFrame(st.session_state.historico, columns=["Multiplicador"])
st.line_chart(df)

# Previsão
st.subheader("🔮 Próxima Previsão")
proxima, nivel = prever_multiplicador(st.session_state.historico)
st.markdown(f"**Multiplicador Previsto:** {proxima:.2f}x")
st.markdown(f"**Nível de Confiança:** {nivel}")

# Adicionar nova entrada
if st.button("➡️ Adicionar Nova Entrada Aleatória"):
    nova = round(random.uniform(1.0, 50.0), 2)
    st.session_state.historico.append(nova)
    if len(st.session_state.historico) > 50:
        st.session_state.historico.pop(0)
    st.experimental_rerun()

# Rodapé
st.markdown("---")
st.markdown("Desenvolvido por **RicardoM-21** | App beta com lógica preditiva experimental")

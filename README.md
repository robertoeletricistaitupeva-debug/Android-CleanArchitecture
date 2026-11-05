 
=======import streamlit as st
import pandas as pd
import numpy as np
from datetime import datetime

# ⚙️ Configuração — Otimizado para celular
st.set_page_config(
    page_title="Trade do Futuro",
    page_icon="🚀",
    layout="centered",
    initial_sidebar_state="collapsed"
)

# 🎨 Estilo — Tema escuro igual à imagem
st.markdown("""
<style>
    * { box-sizing: border-box; }
    .stApp {
        background-color: #12131a;
        color: #e5e7eb;
    }
    .card {
        background-color: #1f2937;
        border-radius: 16px;
        padding: 20px;
        margin: 12px 0;
    }
    .valor-grande {
        font-size: 42px;
        font-weight: 800;
        color: #ffffff;
    }
    .lucro-positivo {
        color: #4ade80;
        font-size: 18px;
    }
    .conta-demo {
        text-align: right;
        color: #9ca3af;
        font-size: 16px;
    }
    .sinal-verde {
        background-color: #16a34a;
        color: white;
        padding: 16px;
        border-radius: 12px;
        text-align: center;
        font-size: 22px;
        font-weight: bold;
        margin: 10px 0;
    }
    .sinal-vermelho {
        background-color: #dc2626;
        color: white;
        padding: 16px;
        border-radius: 12px;
        text-align: center;
        font-size: 22px;
        font-weight: bold;
        margin: 10px 0;
    }
    .btn-principal {
        background-color: #22c55e;
        color: white;
        font-size: 18px;
        font-weight: bold;
        border-radius: 12px;
        padding: 14px;
        border: none;
        width: 100%;
    }
    .btn-secundario {
        background-color: #374151;
        color: white;
        font-size: 18px;
        border-radius: 12px;
        padding: 14px;
        border: none;
        width: 100%;
    }
    .aviso {
        background-color: #1e3a5f;
        border-left: 4px solid #3b82f6;
        padding: 12px;
        border-radius: 8px;
        font-size: 14px;
        color: #bfdbfe;
        margin-top: 20px;
    }
    .rodape {
        text-align: center;
        font-size: 12px;
        color: #6b7280;
        margin-top: 30px;
    }
</style>
""", unsafe_allow_html=True)

# 🚀 Tela de Boas-Vindas
if 'iniciou' not in st.session_state:
    st.markdown("""
    <div style='text-align: center; padding: 60px 20px;'>
        <h1 style='font-size: 60px; margin: 0;'>🚀</h1>
        <h1 style='font-size: 28px; margin: 10px 0;'>Trade do Futuro</h1>
        <p style='color: #9ca3af; font-size: 16px;'>Analisador Inteligente de Gráficos</p>
    </div>
    """, unsafe_allow_html=True)
    
    if st.button("✨ Abrir Aplicativo", type="primary", use_container_width=True):
        st.session_state.iniciou = True
        st.rerun()
    
    st.markdown("""
    <div class='aviso'>
    ⚠️ <strong>Aviso:</strong> Esta é uma ferramenta de análise educacional. Não é uma plataforma de investimentos. Use com responsabilidade.
    </div>
    """, unsafe_allow_html=True)
    st.stop()

# 📊 Tela Principal
st.markdown("<h2 style='font-size: 22px; margin-bottom: 5px;'>Investimento atual</h2>", unsafe_allow_html=True)

# Cartão com saldo
st.markdown("""
<div class='card'>
    <div class='conta-demo'>Conta demo</div>
    <div class='valor-grande'>$1,956.72</div>
    <div class='lucro-positivo'>Lucro +$237.90</div>
</div>
""", unsafe_allow_html=True)

# Área do Ativo e Tempo
col1, col2 = st.columns([1, 3])
with col1:
    st.markdown("""
    <div style='width: 70px; height: 70px; border-radius: 50%; border: 4px solid #22c55e; 
         display: flex; align-items: center; justify-content: center; 
         font-size: 16px; font-weight: bold;'>
        00:15
    </div>
    """, unsafe_allow_html=True)
with col2:
    st.markdown("""
    <div>
        <h3 style='margin: 0; font-size: 20px;'>Ondo (OTC)</h3>
        <p style='color: #9ca3af; margin: 5px 0;'>Indicador: RSI • Confiança: 87%</p>
    </div>
    """, unsafe_allow_html=True)

# Configurações
st.markdown("""
<div class='card'>
    <p style='margin: 5px 0;'><strong>💵 Valor:</strong> $6.00</p>
    <p style='margin: 5px 0;'><strong>📋 Estratégia:</strong> Conservadora</p>
    <p style='margin: 5px 0;'><strong>🎯 Limite de lucro:</strong> Desligado</p>
</div>
""", unsafe_allow_html=True)

# 📈 Sinal de Análise
st.markdown("<h3 style='font-size: 18px; margin-top: 20px;'>📊 Sinal de Análise</h3>", unsafe_allow_html=True)

sinal = st.radio("Qual a leitura do gráfico?", 
                 ["🟢 COMPRAR ⬆️", "🔴 VENDER ⬇️"], 
                 label_visibility="collapsed")

if sinal == "🟢 COMPRAR ⬆️":
    st.markdown("<div class='sinal-verde'>🟢 COMPRAR ⬆️</div>", unsafe_allow_html=True)
else:
    st.markdown("<div class='sinal-vermelho'>🔴 VENDER ⬇️</div>", unsafe_allow_html=True)

# Botões de Ação
col_a, col_b = st.columns(2)
with col_a:
    if st.button("📊 Mostrar Gráfico", use_container_width=True):
        st.info("Faça upload dos dados do gráfico para visualizar")
with col_b:
    if st.button("⏹️ Parar Análise", use_container_width=True):
        st.warning("Análise interrompida")

# Aviso Importante
st.markdown("""
<div class='aviso'>
<strong>⚠️ AVISO IMPORTANTE:</strong><br>
Este aplicativo é uma ferramenta de análise educacional. <strong>Não</strong> se conecta à IQ Option e <strong>não</strong> executa operações automaticamente. 
Use os sinais como referência apenas — você é responsável por suas decisões de negociação. Nenhum resultado é garantido. Negocie com responsabilidade.
</div>
""", unsafe_allow_html=True)

# Placar de Controle
with st.expander("📋 Meu Controle de Resultados"):
    vitorias = st.number_input("Vitórias", min_value=0, step=1)
    derrotas = st.number_input("Derrotas", min_value=0, step=1)
    total = vitorias + derrotas
    if total > 0:
        percentual = (vitorias / total) * 100
        st.write(f"**Total:** {total} operações")
        st.write(f"**Aproveitamento:** {percentual:.1f}%")

# Rodapé
st.markdown("""
<div class='rodape'>
Trade do Futuro — Ferramenta de Análise Educacional<br>
Versão 1.0 • Atualizado em 04/11/2026
</div>
""", unsafe_allow_html=True)
==================

## New version available written in Kotlin:
[Architecting Android… Reloaded](https://fernandocejas.com/2018/05/07/architecting-android-reloaded/)

Introduction
-----------------
This is a sample app that is part of a blog post I have written about how to architect android application using the Uncle Bob's clean architecture approach. 

[Architecting Android…The clean way?](http://fernandocejas.com/2014/09/03/architecting-android-the-clean-way/)

[Architecting Android…The evolution](http://fernandocejas.com/2015/07/18/architecting-android-the-evolution/)

[Tasting Dagger 2 on Android](http://fernandocejas.com/2015/04/11/tasting-dagger-2-on-android/)

[Clean Architecture…Dynamic Parameters in Use Cases](http://fernandocejas.com/2016/12/24/clean-architecture-dynamic-parameters-in-use-cases/)

[Demo video of this sample](http://youtu.be/XSjV4sG3ni0)

Clean architecture
-----------------
![http://fernandocejas.com/2015/07/18/architecting-android-the-evolution/](https://github.com/android10/Sample-Data/blob/master/Android-CleanArchitecture/clean_architecture.png)

Architectural approach
-----------------
![http://fernandocejas.com/2015/07/18/architecting-android-the-evolution/](https://github.com/android10/Sample-Data/blob/master/Android-CleanArchitecture/clean_architecture_layers.png)

Architectural reactive approach
-----------------
![http://fernandocejas.com/2015/07/18/architecting-android-the-evolution/](https://github.com/android10/Sample-Data/blob/master/Android-CleanArchitecture/clean_architecture_layers_details.png)

Local Development
-----------------

Here are some useful Gradle/adb commands for executing this example:

 * `./gradlew clean build` - Build the entire example and execute unit and integration tests plus lint check.
 * `./gradlew installDebug` - Install the debug apk on the current connected device.
 * `./gradlew runUnitTests` - Execute domain and data layer tests (both unit and integration).
 * `./gradlew runAcceptanceTests` - Execute espresso and instrumentation acceptance tests.
 
Discussions
-----------------

Refer to the issues section: https://github.com/android10/Android-CleanArchitecture/issues
 

Code style
-----------

Here you can download and install the java codestyle.
https://github.com/android10/java-code-styles


License
--------

    Copyright 2018 Fernando Cejas

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.


![http://www.fernandocejas.com](https://github.com/android10/Sample-Data/blob/master/android10/android10_logo_big.png)

[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-Android--CleanArchitecture-brightgreen.svg?style=flat)](https://android-arsenal.com/details/3/909)

<a href="https://www.buymeacoffee.com/android10" target="_blank"><img src="https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png" alt="Buy Me A Coffee" style="height: auto !important;width: auto !important;" ></a>

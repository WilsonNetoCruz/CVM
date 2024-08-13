# CVM 

import streamlit as st
import pandas as pd
import plotly.express as px

st.set_page_config(layout='wide')

##############################################################################################

# pesquisar o portal dados abertos cvm
# Base de Dados
# Arquivos CSV & .zip

# ITR - FORMULÁRIO DE INFORMAÇÕES TRIMESTRAIS - desde 2011
# DFP - FORMULÁRIO DE DEMONSTRAÇÕES FINANCEIRAS PADRONIZADAS - desde 2010

'''
Balanço Patrimonial Ativo (BPA)
Balanço Patrimonial Passivo (BPP)
Demonstração de Fluxo de Caixa - Método Direto (DFC-MD)
Demonstração de Fluxo de Caixa - Método Indireto (DFC-MI)
Demonstração das Mutações do Patrimônio Líquido (DMPL)
Demonstração de Resultado (DRE)
Demonstração de Valor Adicionado (DVA)
'''

# Indicadores de Liquidez
'''
Corrente
Imediata
Seca
Geral
'''

# !pip install wget

import pandas as pd
import wget
from zipfile import ZipFile

url_base = 'https://dados.cvm.gov.br/dados/CIA_ABERTA/DOC/DFP/DADOS/'

empresa0 = 'Iguá' # 'GGBR3' #  ['AAPL34', 'BOVA11', 'BPAC11', 'BRBI11', 'JPMC34', 'MRFG3', 'MSFT34', 'PRIO3', 'SIMH3', 'VALE3', 'VIVA3', 'WEGE3']

nempresa = 23175

# Dados Anuais

# DFP

# Lista com os anos
arquivos_zip = []
for ano in range(2010,2025):
  arquivos_zip.append(f'dfp_cia_aberta_{ano}.zip')

arquivos_zip

'''
# Download de todos os arquivos
for arq in arquivos_zip:
  wget.download(url_base + arq)
'''

import requests

for arq in arquivos_zip:
    response = requests.get(url_base + arq)
    with open(arq, "wb") as f:
        f.write(response.content)

import os

import zipfile

output_directory = "CVM-dfp"

if not os.path.exists(output_directory):
    os.makedirs(output_directory)


    #os.makedirs(output_directory)
for arq in arquivos_zip:


    try:
        with zipfile.ZipFile(arq, 'r') as zip_file:
            # Extract all files from the ZIP archive to the output directory
            zip_file.extractall(output_directory)
        print(f"Extracted files from {arq} to {output_directory}")
    except zipfile.BadZipFile:
        print(f"Error extracting {arq}: File is not a valid zip file")


    except Exception as e:
        print(f"Error extracting {arq}: {e}")

'''
# Extraindo os arquivos zip e criando pasta cvm
for arq in arquivos_zip:
  ZipFile(arq, 'r').extractall('CVM-dfp')
  '''

# !mkdir DADOS-dfp
import os

# Nome do diretório que você quer criar
directory = "DADOS-dfp"

# Cria o diretório
os.makedirs(directory, exist_ok=True)

print(f"Diretório '{directory}' criado com sucesso!")
# segue

import pandas as pd

# List of prefixes to process
nomes = ['BPA_con', 'BPP_con']  # Add 'DRE_con' if needed

# Iterate through each prefix
for nome in nomes:
    arquivo = pd.DataFrame()  # Initialize an empty DataFrame

    # Loop through the years from 2010 to 2023 (inclusive)
    for ano in range(2010, 2024):
        file_path = f'CVM-dfp/dfp_cia_aberta_{nome}_{ano}.csv'

        # Check if the file exists before attempting to read it
        if os.path.exists(file_path):
            # Read CSV files for each year
            data = pd.read_csv(file_path, sep=';', decimal=',', encoding='ISO-8859-1')

            # Concatenate data to the DataFrame
            arquivo = pd.concat([arquivo, data])
        else:
            print(f"File not found: {file_path}")

    # Save the concatenated data as a new CSV file in 'DADOS-dfp' directory
    arquivo.to_csv(f'DADOS-dfp/dfp_cia_aberta_{nome}_2010-2025.csv', index=False)


'''
# Criando arquivos históricos  ## Deixar apenas o necessário
nomes = ['BPA_con', 'BPP_con'] # DRE_con
for nome in nomes:
  arquivo = pd.DataFrame()
  for ano in range(2010, 2024):
    arquivo = pd.concat([arquivo, pd.read_csv(f'CVM-dfp/dfp_cia_aberta_{nome}_{ano}.csv', sep=';', decimal=',', encoding='ISO-8859-1')])
  arquivo.to_csv(f'DADOS-dfp/dfp_cia_aberta_{nome}_2010-2023.csv', index=False)
  '''

# pd.read_csv('CVM/itr_cia_aberta_BPA_con_2011.csv', sep=';', decimal=',', encoding='ISO-8859-1')

# BPA

## BPA

bpa = pd.read_csv('/content/DADOS-dfp/dfp_cia_aberta_BPA_con_2010-2025.csv')

# Filtrar e pegar o último exercício
bpa = bpa[bpa['ORDEM_EXERC'] == "ÚLTIMO"]

bpa.tail()

## CD_CVM

empresas = bpa[['DENOM_CIA', 'CD_CVM']].drop_duplicates().set_index('CD_CVM')

empresas

from google.colab.data_table import DataTable

DataTable(empresas)

## Empresa

# Filtrar código da emoresa escolhida
empresa_bpa = bpa[bpa['CD_CVM'] == nempresa]

empresa_bpa

DataTable(empresa_bpa[['CD_CONTA', 'DS_CONTA']].drop_duplicates().set_index('CD_CONTA'))

AC = empresa_bpa[empresa_bpa['CD_CONTA'] == '1.01']
AC.head()

AC.index = pd.to_datetime(AC['DT_REFER'])

AC

# BPP

## BPP

bpp = pd.read_csv('/content/DADOS-dfp/dfp_cia_aberta_BPP_con_2010-2025.csv')

# Filtrar e pegar o último exercício
bpp = bpp[bpp['ORDEM_EXERC'] == "ÚLTIMO"]

bpp.head()

## CD_CVM

empresas = bpp[['DENOM_CIA', 'CD_CVM']].drop_duplicates().set_index('CD_CVM')

empresas # Confere o CD_CVM

DataTable(empresas)

## Empresa

# Filtrar código da emoresa escolhida
empresa_bpp = bpp[bpp['CD_CVM'] == nempresa]

empresa_bpp

DataTable(empresa_bpp[['CD_CONTA', 'DS_CONTA']].drop_duplicates().set_index('CD_CONTA'))

PC = empresa_bpp[empresa_bpp['CD_CONTA'] == '2.01']
PC.head()

PC.index = pd.to_datetime(PC['DT_REFER'])

PC

# Liquidez

# BPA (Balanço Patrimonial Ativo)
# 1.01 --> Ativo Circulante
# 1.02.01 --> Ativo Realizável a Longo Prazo
# 1.01.01 --> Caixa e Equivalente de Caixa
# 1.01.04 --> Estoques

# BPP (Balanço Patrimonial Passivo)
# 2.01 --> Passivo Circulante
# 2.02.04 --> Provisões

## Corrente

# LC = AC / PC

AC.rename({'VL_CONTA':'Ativo_Circulante'}, axis=1, inplace=True)

PC.rename({'VL_CONTA':'Passivo_Circulante'}, axis=1, inplace=True)

LC = pd.DataFrame(AC['Ativo_Circulante']).join(pd.DataFrame(PC['Passivo_Circulante']), how='outer')

LC['Liquidez_Corrente'] = AC['Ativo_Circulante'] / PC['Passivo_Circulante']
LC

import plotly.graph_objects as go

fig = go.Figure()
fig.add_trace(go.Scatter(x=LC.index, y=LC['Liquidez_Corrente'], name='Liquidez_Corrente'))
fig.show()

## Seca

# LS = (AC - E) / PC

E = empresa_bpa[empresa_bpa['CD_CONTA'] == '1.01.04']
E.index = pd.to_datetime(E['DT_REFER'])

E.rename({'VL_CONTA':'Estoques'}, axis=1, inplace=True)

LS = pd.DataFrame(AC['Ativo_Circulante']).join(pd.DataFrame(PC['Passivo_Circulante']), how='outer')
LS = LS.join(pd.DataFrame(E['Estoques']), how='outer')

LS['Liquidez_Seca'] = (AC['Ativo_Circulante'] - E['Estoques']) / PC['Passivo_Circulante']
LS

fig = go.Figure()
fig.add_trace(go.Scatter(x=LS.index, y=LS['Liquidez_Seca'], name='Liquidez_Seca'))
fig.show()

## Imediata

# LI = D / PC

D = empresa_bpa[empresa_bpa['CD_CONTA'] == '1.01.01']
D.index = pd.to_datetime(D['DT_REFER'])

D.rename({'VL_CONTA':'Disponibilidades'}, axis=1, inplace=True)

LI = pd.DataFrame(D['Disponibilidades']).join(pd.DataFrame(PC['Passivo_Circulante']), how='outer')

LI['Liquidez_Imediata'] = D['Disponibilidades'] / PC['Passivo_Circulante']
LI

fig = go.Figure()
fig.add_trace(go.Scatter(x=LI.index, y=LI['Liquidez_Imediata'], name='Liquidez_Imediata'))
fig.show()

## Geral

# LG = (AC + RLP) / (PC + ELP)

RLP = empresa_bpa[empresa_bpa['CD_CONTA'] == '1.02.01']
RLP.index = pd.to_datetime(RLP['DT_REFER'])

RLP.rename({'VL_CONTA':'Realizavel'}, axis=1, inplace=True)

ELP = empresa_bpp[empresa_bpp['CD_CONTA'] == '2.02.04']
ELP.index = pd.to_datetime(ELP['DT_REFER'])

ELP.rename({'VL_CONTA':'Exigivel'}, axis=1, inplace=True)

LG1 = pd.DataFrame(AC['Ativo_Circulante']).join(pd.DataFrame(RLP['Realizavel']), how='outer')
LG2 = pd.DataFrame(PC['Passivo_Circulante']).join(pd.DataFrame(ELP['Exigivel']), how='outer')
LG = LG1.join(LG2, how='outer')

LG['Liquidez_Geral'] = (AC['Ativo_Circulante'] + RLP['Realizavel']) / (PC['Passivo_Circulante'] + ELP['Exigivel'])
LG

fig = go.Figure()
fig.add_trace(go.Scatter(x=LG.index, y=LG['Liquidez_Geral'], name='Liquidez_Geral'))
fig.show()

# Gráficos

fig = go.Figure()
fig.add_trace(go.Scatter(x=LG.index, y=AC['Ativo_Circulante'], name='Ativo_Circulante'))
fig.add_trace(go.Scatter(x=LG.index, y=PC['Passivo_Circulante'], name='Passivo_Circulante'))
fig.add_trace(go.Scatter(x=LG.index, y=RLP['Realizavel'], name='Realizavel'))
fig.add_trace(go.Scatter(x=LG.index, y=ELP['Exigivel'], name='Exigivel'))
fig.show()

fig = go.Figure()
fig.add_trace(go.Scatter(x=LC.index, y=LC['Liquidez_Corrente'], name='Liquidez_Corrente'))
fig.add_trace(go.Scatter(x=LS.index, y=LS['Liquidez_Seca'], name='Liquidez_Seca'))
fig.add_trace(go.Scatter(x=LI.index, y=LI['Liquidez_Imediata'], name='Liquidez_Imediata'))
fig.add_trace(go.Scatter(x=LG.index, y=LG['Liquidez_Geral'], name='Liquidez_Geral'))
fig.show()

# Dados Trimestrais

# ITR

url_base = 'https://dados.cvm.gov.br/dados/CIA_ABERTA/DOC/ITR/DADOS/'

# Lista com nomes dos ativos
arquivos_zip = []
for ano in range(2020,2025):
  arquivos_zip.append(f'itr_cia_aberta_{ano}.zip')

arquivos_zip

'''
# Download de todos os arquivos
for arq in arquivos_zip:
  wget.download(url_base + arq)
'''

import requests

for arq in arquivos_zip:
    response = requests.get(url_base + arq)
    with open(arq, "wb") as f:
        f.write(response.content)

# Extraindo os arquivos zip e criando pasta cvm
for arq in arquivos_zip:
  ZipFile(arq, 'r').extractall('CVM-itr')

# !mkdir DADOS-itr 
import os

# Nome do diretório que você quer criar
directory = "DADOS-itr"

# Cria o diretório
os.makedirs(directory, exist_ok=True)

print(f"Diretório '{directory}' criado com sucesso!")
# segue   

# Criando arquivos históricos
nomes = ['BPA_con', 'BPP_con']
for nome in nomes:
  arquivo = pd.DataFrame()
  for ano in range(2020, 2025):
    arquivo = pd.concat([arquivo, pd.read_csv(f'CVM-itr/itr_cia_aberta_{nome}_{ano}.csv', sep=';', decimal=',', encoding='ISO-8859-1')])
  arquivo.to_csv(f'DADOS-itr/itr_cia_aberta_{nome}_2020-2024.csv', index=False)

# dreitr = pd.read_csv('/content/DADOS-itr/itr_cia_aberta_DRE_con_2011-2020.csv')

# BPA

## BPA

bpa_itr = pd.read_csv('/content/DADOS-itr/itr_cia_aberta_BPA_con_2020-2025.csv')

# Filtrar e pegar o último exercício
bpa_itr = bpa_itr[bpa_itr['ORDEM_EXERC'] == "ÚLTIMO"]

bpa_itr.tail()

## CD_CVM

empresas = bpa_itr[['DENOM_CIA', 'CD_CVM']].drop_duplicates().set_index('CD_CVM')

empresas

DataTable(empresas)

## Empresa

# Filtrar código da emoresa escolhida
empresa_bpa_itr = bpa_itr[bpa_itr['CD_CVM'] == nempresa]

empresa_bpa_itr

DataTable(empresa_bpa_itr[['CD_CONTA', 'DS_CONTA']].drop_duplicates().set_index('CD_CONTA'))

AC_itr = empresa_bpa_itr[empresa_bpa_itr['CD_CONTA'] == '1.01']
AC_itr.head()

AC_itr.index = pd.to_datetime(AC_itr['DT_REFER'])

AC_itr

# BPP

## BPP

bpp_itr = pd.read_csv('/content/DADOS-itr/itr_cia_aberta_BPP_con_2020-2023.csv')

# Filtrar e pegar o último exercício
bpp_itr = bpp_itr[bpp_itr['ORDEM_EXERC'] == "ÚLTIMO"]

bpp_itr.head()

## CD_CVM

empresas = bpp_itr[['DENOM_CIA', 'CD_CVM']].drop_duplicates().set_index('CD_CVM')

empresas # Confere o CD_CVM

DataTable(empresas)

## Empresa

# Filtrar código da emoresa escolhida
empresa_bpp_itr = bpp_itr[bpp_itr['CD_CVM'] == nempresa]

empresa_bpp_itr

DataTable(empresa_bpp_itr[['CD_CONTA', 'DS_CONTA']].drop_duplicates().set_index('CD_CONTA'))

PC_itr = empresa_bpp_itr[empresa_bpp_itr['CD_CONTA'] == '2.01']
PC_itr.head()

PC_itr.index = pd.to_datetime(PC_itr['DT_REFER'])

PC_itr

# Liquidez

# BPA (Balanço Patrimonial Ativo) -- ITR
# 1.01 --> Ativo Circulante
# 1.02.01 --> Ativo Realizável a Longo Prazo
# 1.01.01 --> Caixa e Equivalente de Caixa
# 1.01.04 --> Estoques

# BPP (Balanço Patrimonial Passivo)
# 2.01 --> Passivo Circulante
# 2.02.04 --> Provisões

## Corrente

# LC = AC / PC

AC_itr.rename({'VL_CONTA':'Ativo_Circulante'}, axis=1, inplace=True)

PC_itr.rename({'VL_CONTA':'Passivo_Circulante'}, axis=1, inplace=True)

LC_itr = pd.DataFrame(AC_itr['Ativo_Circulante']).join(pd.DataFrame(PC_itr['Passivo_Circulante']), how='outer')

LC_itr

LC_itr['Liquidez_Corrente'] = LC_itr['Ativo_Circulante'] / LC_itr['Passivo_Circulante']
LC_itr

fig = go.Figure()
fig.add_trace(go.Scatter(x=LC_itr.index, y=LC_itr['Liquidez_Corrente'], name='Liquidez_Corrente'))
fig.show()

## Seca

# LS = (AC - E) / PC

E_itr = empresa_bpa_itr[empresa_bpa_itr['CD_CONTA'] == '1.01.04']
E_itr.index = pd.to_datetime(E_itr['DT_REFER'])

E_itr.rename({'VL_CONTA':'Estoques'}, axis=1, inplace=True)

LS_itr = pd.DataFrame(AC_itr['Ativo_Circulante']).join(pd.DataFrame(PC_itr['Passivo_Circulante']), how='outer')
LS_itr = LS_itr.join(pd.DataFrame(E_itr['Estoques']), how='outer')

LS_itr['Liquidez_Seca'] = (LS_itr['Ativo_Circulante'] - LS_itr['Estoques']) / LS_itr['Passivo_Circulante']
LS_itr

fig = go.Figure()
fig.add_trace(go.Scatter(x=LS_itr.index, y=LS_itr['Liquidez_Seca'], name='Liquidez_Seca'))
fig.show()

## Imediata

# LI = D / PC

D_itr = empresa_bpa_itr[empresa_bpa_itr['CD_CONTA'] == '1.01.01']
D_itr.index = pd.to_datetime(D_itr['DT_REFER'])

D_itr.rename({'VL_CONTA':'Disponibilidades'}, axis=1, inplace=True)

LI_itr = pd.DataFrame(D_itr['Disponibilidades']).join(pd.DataFrame(PC_itr['Passivo_Circulante']), how='outer')

LI_itr['Liquidez_Imediata'] = LI_itr['Disponibilidades'] / LI_itr['Passivo_Circulante']
LI_itr

fig = go.Figure()
fig.add_trace(go.Scatter(x=LI_itr.index, y=LI_itr['Liquidez_Imediata'], name='Liquidez_Imediata'))
fig.show()

## Geral

# LG = (AC + RLP) / (PC + ELP)

RLP_itr = empresa_bpa_itr[empresa_bpa_itr['CD_CONTA'] == '1.02.01']
RLP_itr.index = pd.to_datetime(RLP_itr['DT_REFER'])

RLP_itr.rename({'VL_CONTA':'Realizavel'}, axis=1, inplace=True)

ELP_itr = empresa_bpp_itr[empresa_bpp_itr['CD_CONTA'] == '2.02.04']
ELP_itr.index = pd.to_datetime(ELP_itr['DT_REFER'])

ELP_itr.rename({'VL_CONTA':'Exigivel'}, axis=1, inplace=True)

LG1_itr = pd.DataFrame(AC_itr['Ativo_Circulante']).join(pd.DataFrame(RLP_itr['Realizavel']), how='outer')
LG2_itr = pd.DataFrame(PC_itr['Passivo_Circulante']).join(pd.DataFrame(ELP_itr['Exigivel']), how='outer')
LG_itr = LG1_itr.join(LG2_itr, how='outer')

LG_itr['Liquidez_Geral'] = (LG_itr['Ativo_Circulante'] + LG_itr['Realizavel']) / (LG_itr['Passivo_Circulante'] + LG_itr['Exigivel'])
LG_itr

fig = go.Figure()
fig.add_trace(go.Scatter(x=LG_itr.index, y=LG_itr['Liquidez_Geral'], name='Liquidez_Geral'))
fig.show()

# Gráficos

LC_itr['Liquidez_Corrente'][-1]

LS_itr['Liquidez_Seca'][-1]

LI_itr['Liquidez_Imediata'][-1]

LG_itr['Liquidez_Geral'][-1]

fig = go.Figure()
fig.add_trace(go.Scatter(x=LG_itr.index, y=AC_itr['Ativo_Circulante'], name='Ativo_Circulante'))
fig.add_trace(go.Scatter(x=LG_itr.index, y=PC_itr['Passivo_Circulante'], name='Passivo_Circulante'))
fig.add_trace(go.Scatter(x=LG_itr.index, y=RLP_itr['Realizavel'], name='Realizavel'))
fig.add_trace(go.Scatter(x=LG_itr.index, y=ELP_itr['Exigivel'], name='Exigivel'))
fig.show()

fig = go.Figure()
fig.add_trace(go.Scatter(x=LC_itr.index, y=LC_itr['Liquidez_Corrente'], name='Liquidez_Corrente'))
fig.add_trace(go.Scatter(x=LS_itr.index, y=LS_itr['Liquidez_Seca'], name='Liquidez_Seca'))
fig.add_trace(go.Scatter(x=LI_itr.index, y=LI_itr['Liquidez_Imediata'], name='Liquidez_Imediata'))
fig.add_trace(go.Scatter(x=LG_itr.index, y=LG_itr['Liquidez_Geral'], name='Liquidez_Geral'))
fig.show()

#######################################################################################################


# cÓDIGO E arquivo csv, xlm...
st.write("Hello World")

DataTable(empresas)

df = empresas
#nempresa = 23175

escolha_empresa = st.sidebar.selectbox("DENOM_CIA", df["DENOM_CIA"].unique())

df_filtered = df[df["DENOM_CIA"] == empresas]
df_filtered


#rever e adaptaro ao c[odigo]


# Filtragem de dados

col1, col2, = st.columns(2)
col3, col4, col5 = st.columns(3)


# comentario
# comentario, comentário...
# Funciona?
# 

fig = go.Figure()
fig_Streamlit = fig.add_trace(go.Scatter(x=LG_itr.index, y=AC_itr['Ativo_Circulante'], name='Ativo_Circulante'))
col1.plotly_chart(fig_Streamlit)

'''
fig.add_trace(go.Scatter(x=LG_itr.index, y=PC_itr['Passivo_Circulante'], name='Passivo_Circulante'))
fig.add_trace(go.Scatter(x=LG_itr.index, y=RLP_itr['Realizavel'], name='Realizavel'))
fig.add_trace(go.Scatter(x=LG_itr.index, y=ELP_itr['Exigivel'], name='Exigivel'))
fig.show()

fig = go.Figure()
fig.add_trace(go.Scatter(x=LC_itr.index, y=LC_itr['Liquidez_Corrente'], name='Liquidez_Corrente'))
fig.add_trace(go.Scatter(x=LS_itr.index, y=LS_itr['Liquidez_Seca'], name='Liquidez_Seca'))
fig.add_trace(go.Scatter(x=LI_itr.index, y=LI_itr['Liquidez_Imediata'], name='Liquidez_Imediata'))
fig.add_trace(go.Scatter(x=LG_itr.index, y=LG_itr['Liquidez_Geral'], name='Liquidez_Geral'))
fig.show()
'''
'''
import streamlit as st

# Título da página
st.title("Título do Aplicativo")

# Subtítulo
st.subheader("Subtítulo do Aplicativo")

# Texto simples
st.write("Este é um texto simples que pode incluir variáveis como:", 42)

# Texto em markdown
st.markdown("### Texto em Markdown")
st.markdown("Você pode adicionar [links](https://www.example.com), **negrito**, *itálico* e `código`.")

# Exibir um gráfico de linha
# st.line_chart(data.set_index('Números'))

# Botão
if st.button('Clique aqui'):
    st.write('Botão clicado!')

# Caixa de seleção
if st.checkbox('Mostrar mais informações'):
    st.write("Aqui estão mais informações.")

# Slider
valor = st.slider('Escolha um valor', 0, 100, 50)
st.write(f'Você escolheu: {valor}')

# Entrada de texto
nome = st.text_input('Digite seu nome')
st.write(f'Olá, {nome}!')

# Upload de arquivos
uploaded_file = st.file_uploader("Escolha um arquivo CSV")
if uploaded_file is not None:
    data = pd.read_csv(uploaded_file)
    st.write(data)

# Dividindo em colunas
col1, col2 = st.columns(2)

with col1:
    st.write("Esta é a coluna 1")

with col2:
    st.write("Esta é a coluna 2")

# Barra lateral
st.sidebar.title("Barra Lateral")
st.sidebar.write("Você pode adicionar widgets aqui.")

# Exibir tabelas de dados
st.dataframe(data)  # Tabela interativa
st.table(data)      # Tabela estática
st.write(data)      # Detecção automática do tipo de exibição

# Mensagem de sucesso
st.success("Operação bem-sucedida!")

# Mensagem de erro
st.error("Algo deu errado!")

# Mensagem de aviso
st.warning("Cuidado com esta ação!")

# Mensagem informativa
st.info("Aqui está uma informação importante.")

# Mensagem de exceção
try:
    x = 1 / 0
except ZeroDivisionError as e:
    st.exception(e)
'''

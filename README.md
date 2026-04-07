# Matplotlib
#Pequeno repositório mostrando como a biblioteca matplotlib pode ser útil para análise de dados
#Estarei utilizando um arquivo no excel que fez um comparativo entre a Petrobras e o Itaú 

dados = pd.read_csv("C:/Users/""""""/Downloads/dados/dados.csv") #ponha o nome do seu usuario
dias = dados.index
petro = dados['PETR4']
itau = dados['ITUB4']

fig = plt.figure(figsize=(12, 8))

grid = fig.add_gridspec(2, 2)
ax_linha = fig.add_subplot(grid[0, :]) #Quadro maior ocupante
ax_hist_1 = fig.add_subplot(grid[1, 0]) #Quadro inferior a direita
ax_hist_2 = fig.add_subplot(grid[1, 1]) #Quadro inferior a esquerda

ax_linha.plot(dias, petro, label='Petro', color='green', linestyle='--', marker='.')
ax_linha.plot(dias, itau, label='Itaú', color='orange', linestyle='--', marker='.')

ax_linha.set_title('Cotação - 2025/1')
ax_linha.set_xlabel('Dias')
ax_linha.set_ylabel('Valor da ação (R$)')

ax_hist_1.hist(petro.diff().dropna(), color='green', bins=50)
ax_hist_2.hist(itau.diff().dropna(), color='orange', bins=50)



#Quadro inferior Petrobras
ax_hist_1.hist(petro.diff(), label='Petro', color='green', bins=50)
ax_hist_1.axvline(petro.diff().mean(), color='gray', linestyle='--', linewidth=4)

ax_hist_1.set_xlabel('Variação (R$)')
ax_hist_1.set_ylabel('Frequência')
ax_hist_1.grid('on')

#Quadro inferior Itaú
ax_hist_2.hist(itau.diff(), label='Itaú', color='orange', bins=50)
ax_hist_2.axvline(petro.diff().mean(), color='gray', linestyle='--', linewidth=4)

ax_hist_2.set_xlabel('Variação (R$)')
ax_hist_2.set_ylabel('Frequência')
ax_hist_2.grid('on')

#fig.subtitle('Análise de Ações')
fig.legend()
fig.tight_layout() #Remover espaços desnecessários

#plt.savefig('figura.png') #Salvar a figura

plt.show()

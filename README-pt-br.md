# Desativando o Teclado Interno em Linux Usando `xinput`

Este documento explica como desativar o teclado interno de um notebook em sistemas Linux usando o comando `xinput`. O procedimento é útil em casos específicos e é compatível com distribuições que utilizam o servidor gráfico **Xorg**.

## Quando Usar?

Este método é útil para:
- Substituir o teclado interno por um teclado externo devido a defeitos físicos.
- Prevenir a entrada de dados acidental (ex.: teclado quebrado digitando sozinho).
- Configurações temporárias para testes ou desenvolvimento.

## Pré-requisitos

- Um sistema Linux baseado em Xorg.
- Acesso ao terminal com permissões de usuário comum (ou sudo, dependendo da configuração do sistema).

## Passos para Desativar o Teclado Interno

### 1. Identificar o Dispositivo do Teclado
1. Abra o terminal.
2. Execute o comando:
   ```bash
   xinput list
   ```
3. Na saída, procure pelo dispositivo que representa o teclado interno. Normalmente, ele será algo como **"AT Translated Set 2 keyboard"**.
4. Anote o **ID** associado ao teclado.

### 2. Desativar o Teclado
1. Use o comando abaixo, substituindo `<ID_do_teclado>` pelo número do ID anotado:
   ```bash
   xinput disable <ID_do_teclado>
   ```
2. O teclado interno estará desativado. Teste pressionando algumas teclas.

### 3. Reativar o Teclado (se necessário)
Se quiser reativar o teclado, use:
```bash
xinput enable <ID_do_teclado>
```

## Tornar a Mudança Permanente
Para desativar o teclado automaticamente ao iniciar o sistema:

1. Crie um script:
   ```bash
   sudo nano /etc/profile.d/desativar_teclado.sh
   ```
2. Adicione o seguinte conteúdo:
   ```bash
   #!/bin/bash
   xinput disable <ID_do_teclado>
   ```
3. Torne o script executável:
   ```bash
   sudo chmod +x /etc/profile.d/desativar_teclado.sh
   ```

## Onde Funciona?

### Sistemas Compatíveis
- **Ubuntu** e derivados (Lubuntu, Xubuntu, etc.)
- **Debian**
- **Linux Mint**
- **Fedora** (se configurado para usar Xorg)
- **Manjaro** e outras distribuições baseadas em Arch Linux
- **Pop!_OS**

### Limitações
Este método **não funciona** em:
- Sistemas baseados no servidor gráfico **Wayland**.
- Outros sistemas operacionais, como **macOS** e **Windows** (que possuem métodos alternativos para desativar o teclado).

## Considerações Finais
- Este procedimento não é permanente, a menos que seja configurado com scripts de inicialização.
- Em sistemas com Wayland, será necessário usar outras ferramentas ou métodos.

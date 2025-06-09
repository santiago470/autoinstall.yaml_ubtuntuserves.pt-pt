# Instalação Automática do Ubuntu Server (pt-PT)

Este repositório contém um ficheiro `autoinstall.yaml` para automatizar a instalação do **Ubuntu Server** com configurações específicas para o utilizador `santiago470`.

---

## Configurações Incluídas

O ficheiro `autoinstall.yaml` configura o Ubuntu Server com as seguintes características:

* **Idioma e Teclado:** Português de Portugal (`pt_PT`).
* **Nome do Servidor (Hostname):** `snats-server`.
* **Utilizador Padrão:** `snats-server` com permissões `sudo`.
    * **Senha:** A senha é definida como `0326` (o hash SHA-512 desta senha está incluído no `autoinstall.yaml`).
        **ATENÇÃO:** Esta é uma senha muito fraca e **NÃO é recomendada para ambientes de produção**. Use apenas para testes ou ambientes locais isolados.
* **Rede:** Configurada para obter um endereço IP via DHCP.
* **Armazenamento:** Layout de disco padrão (usando todo o disco disponível).
* **Ferramentas de VM:** Instala automaticamente os `open-vm-tools` para melhor integração com o VirtualBox (redimensionamento de tela, copiar/colar, etc.).

---

## Como Usar

Para usar este ficheiro `autoinstall.yaml` e instalar o Ubuntu Server automaticamente numa máquina virtual (ex: VirtualBox):

### 1. Descarregar a ISO do Ubuntu Server

* Descarregue a imagem ISO da versão LTS do Ubuntu Server (ex: 22.04 LTS ou 24.04 LTS) do site oficial da Ubuntu: [ubuntu.com/download/server](https://ubuntu.com/download/server)

### 2. Criar a Máquina Virtual

* Crie uma nova máquina virtual no seu software de virtualização (ex: VirtualBox).
* Anexe a ISO do Ubuntu Server descarregada como disco de arranque.
* **Não inicie a instalação ainda.**

### 3. Obter o URL "Raw" do `autoinstall.yaml`

Para que o instalador do Ubuntu possa aceder a este ficheiro, ele precisa de um URL direto (RAW).

* Aceda a este repositório no GitHub.
* Clique no ficheiro `autoinstall.yaml`.
* No canto superior direito do conteúdo do ficheiro, clique no botão **"Raw"**.
* Copie o URL completo que aparece na barra de endereços do seu navegador. Deverá ser algo parecido com:
    `https://raw.githubusercontent.com/santiago470/autoinstall.yaml_ubtuntuserves.pt-pt/main/autoinstall.yaml`

### 4. Iniciar a Instalação Automática

* Inicie a sua máquina virtual.
* Quando a tela de boot do Ubuntu Server aparecer (com opções como "Try or Install Ubuntu Server"), selecione a primeira opção e pressione a tecla **`e`** para editar os parâmetros de boot.
* Procure a linha que começa com `linux /casper/vmlinuz` (ou similar).
* No final dessa linha (antes de `---`), adicione o seguinte parâmetro, substituindo `SEU_URL_RAW_DO_GITHUB` pelo URL que copiou no passo 3:
    ```
    autoinstall ds=nocloud-net;s=SEU_URL_RAW_DO_GITHUB
    ```
    Exemplo completo:
    ```
    autoinstall ds=nocloud-net;s=[https://raw.githubusercontent.com/santiago470/autoinstall.yaml_ubtuntuserves.pt-pt/main/autoinstall.yaml](https://raw.githubusercontent.com/santiago470/autoinstall.yaml_ubtuntuserves.pt-pt/main/autoinstall.yaml)
    ```
* Pressione **`F10`** ou **`Ctrl+X`** para iniciar o boot.

O instalador do Ubuntu Server deverá agora iniciar o processo de instalação totalmente automatizado com base nas configurações do seu `autoinstall.yaml`. A VM reiniciará após a conclusão e estará pronta a usar.

---

## Contribuições

Sinta-se à vontade para fazer `fork` deste repositório, fazer melhorias e enviar `pull requests`.

---

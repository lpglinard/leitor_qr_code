# Documentação do Aplicativo: Leitor de QR Code  


Aplicativo desenvolvido em **Dart com Flutter** que utiliza a câmera do dispositivo para escanear códigos QR e exibir as informações decodificadas em tempo real. 
Ele pode ser utilizado para diversos fins, como leitura de URLs, textos ou outros tipos de dados codificados em QR Codes.

---

## **Funcionalidades Principais**  

1. **Escaneamento de QR Code:**  
   - A câmera do dispositivo é usada para capturar e ler QR Codes.  
   - Os dados são processados e exibidos imediatamente na tela.  

2. **Registro de Leituras:**  
   - Os QR Codes lidos são salvos para visualização posterior.  
   - Oferece a opção de remover itens salvos do registro.  


---

## **Tecnologias Utilizadas**  

- **Linguagem de Programação:** Dart  
- **Framework:** Flutter  
- **Bibliotecas/Plugins:**  
  - `flutter_barcode_scanner`: Para escaneamento de QR Code.  
  - `shared_preferences`: Para armazenamento do histórico local.  
  - `provider`: Gerenciamento de estado para a interface.  

---

## **Requisitos de Sistema**  

- **Android:** Versão 5.0 (Lollipop) ou superior.  
- **iOS:** Versão 11.0 ou superior.  
- **Permissões:**  
  - Acesso à câmera.  
  - Armazenamento (opcional, para salvar históricos).  

---

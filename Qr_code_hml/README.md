# Projeto em Modo de Manutenção

Como os frameworks subjacentes deste pacote, [zxing para Android](https://github.com/zxing/zxing) e [MTBBarcodescanner para iOS](https://github.com/mikebuss/MTBBarcodeScanner), não estão mais sendo mantidos, este plugin agora está apenas em modo de manutenção. Somente correções de bugs e pequenas melhorias serão consideradas.

Estou desenvolvendo um novo plugin, [mobile_scanner](https://pub.dev/packages/mobile_scanner), que utiliza a versão mais recente do MLKit para detecção de códigos de barras e QR codes. No Android, ele também usa a versão mais recente do CameraX e, no iOS, a AVFoundation nativa para melhor desempenho da câmera.

# Scanner de QR Code

Um scanner de QR code que funciona tanto no iOS quanto no Android, embutindo nativamente a visualização da plataforma dentro do Flutter. A integração com o Flutter é fluida, muito melhor do que pular para uma Activity nativa ou um ViewController para realizar a leitura.

## Obter Código QR

Quando um código QR é reconhecido, o texto identificado será definido em 'result' do tipo `Barcode`, que contém o texto de saída como a propriedade 'code' do tipo `String` e o tipo de código escaneado como a propriedade 'format', que é um enum `BarcodeFormat`, definido na biblioteca.

```dart
class _QRViewExampleState extends State<QRViewExample> {
  final GlobalKey qrKey = GlobalKey(debugLabel: 'QR');
  Barcode? result;
  QRViewController? controller;

  // Para que o hot reload funcione, precisamos pausar a câmera se a plataforma
  // for Android, ou retomar a câmera se a plataforma for iOS.
  @override
  void reassemble() {
    super.reassemble();
    if (Platform.isAndroid) {
      controller!.pauseCamera();
    } else if (Platform.isIOS) {
      controller!.resumeCamera();
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Column(
        children: <Widget>[
          Expanded(
            flex: 5,
            child: QRView(
              key: qrKey,
              onQRViewCreated: _onQRViewCreated,
            ),
          ),
          Expanded(
            flex: 1,
            child: Center(
              child: (result != null)
                  ? Text(
                      'Tipo de Código: ${describeEnum(result!.format)}   Dados: ${result!.code}')
                  : Text('Escaneie um código'),
            ),
          )
        ],
      ),
    );
  }

  void _onQRViewCreated(QRViewController controller) {
    this.controller = controller;
    controller.scannedDataStream.listen((scanData) {
      setState(() {
        result = scanData;
      });
    });
  }

  @override
  void dispose() {
    controller?.dispose();
    super.dispose();
  }
}

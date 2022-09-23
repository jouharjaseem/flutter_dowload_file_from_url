import 'package:flutter_downloader/flutter_downloader.dart';


   _permition();
   IsolateNameServer.registerPortWithName(
        _port.sendPort, 'downloader_send_port');
    _port.listen((dynamic data) {
      String id = data[0];
      DownloadTaskStatus status = data[1];
      int progress = data[2];
      setState(() {});
    });

    FlutterDownloader.registerCallback(downloadCallback);
    
    
    @override
  void dispose() {
    IsolateNameServer.removePortNameMapping('downloader_send_port');
    super.dispose();
  }

  static void downloadCallback(
      String id, DownloadTaskStatus status, int progress) {
    final SendPort send =
        IsolateNameServer.lookupPortByName('downloader_send_port')!;
    send.send([id, status, progress]);
  }
  
  /* final status = await Permission.storage.request();

                              if (status.isGranted) {
                                final externalDir =
                                    await getExternalStorageDirectory();

                                final id = await FlutterDownloader.enqueue(
                                  url: model.base_url +
                                      "/uploads/homework/" +
                                      content[index]["filename"],
                                  fileName: content[index]["filename"],
                                  savedDir: externalDir!.path,
                                  showNotification: true,
                                  openFileFromNotification: true,
                                );
                              } else {
                                print('Permission Denied');
                              }

                              */
                              
  _permition() async {
    WidgetsFlutterBinding.ensureInitialized();
    await Permission.storage.request();
  }

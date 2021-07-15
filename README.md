# Uso de NotificationCenter en Swift

## 1 - Posteo la notificacion a ser recivida en cualquier lugar de mi app

```swift
NotificationCenter.default.post(name: NSNotification.Name.init(rawValue: "KEY"), object: self)
```
NOTA: el self es del viewcontroller donde se registra la notificación

## 2 - En ViewController del observador declaramos la variable que contendra el observador si no queremos que se afecte este viewController si se ejecuta el mismo NotificationCenter por otro ViewController

```swift
var observer: NSObjectProtocol?
```

## 3 - Registro mi observador

```swift
override func viewDidAppear(_ animated: Bool) {
	super.viewDidAppear(true)

	observer = NotificationCenter.default.addObserver(forName: NSNotification.Name.init("IDENTIFICADOR"), object: nil, queue: OperationQueue.main, using: { (Notification) in

		let vc = Notification.object as!  DateModalViewController

		if let dt = vc.dateSelected{
			self.dateLabel.text = dt
		}else{
			self.dateLabel.text = "No esta funcionando"
		}
	})
}
```

## 4 - Quito el registro de mi observador

```swift
override func viewDidDisappear(_ animated: Bool) {
    super.viewDidDisappear(true)

    if let obj = observer{
        NotificationCenter.default.removeObserver(obj)
    }
}
```

# Como Recivir notificaciones en Swift UI

```
.onReceive(NotificationCenter.default.publisher(for: NSNotification.Name.init(Env.NC_KEY_REFRESH_WIDGET)) ) { notification in


	if let filter = notification.object as? FilterModel{
	loadData(filter: filter)

	print("Se ejcuto 138")
	}
}
```

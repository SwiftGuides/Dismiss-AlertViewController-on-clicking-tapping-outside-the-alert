# Dismiss-AlertViewController-on-clicking-tapping-outside-the-alert
It will dismiss the alert when clicking outside of the alert popup



```swift
extension  UIViewController {

    func popupAlertWithActionTapOutSideDismiss(title: String?, message: String?, actionTitles:[String?], actions:[((UIAlertAction) -> Void)?]) {
        let alert = UIAlertController(title: title, message: message, preferredStyle: .alert)
        for (index, title) in actionTitles.enumerated() {
            let action = UIAlertAction(title: title, style: .default, handler: actions[index])
            alert.addAction(action)
        }
        //Make a completion like this perform callback actions of dismiss 
        UIApplication.topViewController()?.present(alert, animated: true, completion: {
            
            alert.view.superview?.isUserInteractionEnabled = true
            alert.view.superview?.addGestureRecognizer(UITapGestureRecognizer(target: self, action: #selector(self.alertClose(gesture:))))
        })
    }
    
    //Dismiss function 
   @objc func alertClose(gesture: UITapGestureRecognizer) {
    self.dismiss(animated: true, completion: nil)
    }

}

```

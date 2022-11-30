
 
 // ******* svg convert png ******* *******
 
 let svg = URL(string: strQRCode)!
        if let data = try? Data(contentsOf: svg)
        {
            imgQRCode.isHidden = false
            let receivedimage: SVGKImage = SVGKImage(data: data)
            imgQRCode.image = receivedimage.uiImage
        }
        else
        {
            imgQRCode.isHidden = true
        }
     
     
     
        // ******* extension svg convert png *******
        extension UIImageView {
func downloadedsvg(from url: URL, contentMode mode: UIView.ContentMode = .scaleAspectFit) {
    contentMode = mode
    URLSession.shared.dataTask(with: url) { data, response, error in
        guard
            let httpURLResponse = response as? HTTPURLResponse, httpURLResponse.statusCode == 200,
            let mimeType = response?.mimeType, mimeType.hasPrefix("image"),
            let data = data, error == nil,
            let receivedicon: SVGKImage = SVGKImage(data: data),
            let image = receivedicon.uiImage
            else { return }
        DispatchQueue.main.async() {
            self.image = image
        }
    }.resume()
}
}
        
  
 
  
  // ******* activityViewController *******
        
        @IBAction func clickedShareQRCode(_ sender: Any) {
        
        let imageToShare = [imgQRCode.image!]
        let activityViewController = UIActivityViewController(activityItems: imageToShare as [Any], applicationActivities: nil)
        activityViewController.popoverPresentationController?.sourceView = self.view // so that iPads won't crash
        // exclude some activity types from the list (optional)
        // present the view controller
        self.present(activityViewController, animated: true, completion: nil)
        
    }

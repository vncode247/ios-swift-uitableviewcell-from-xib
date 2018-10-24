[![Watch the video](https://i.imgur.com/Zq7FXzP.png)](https://youtu.be/A7J0AmtVABg)

# ios-swift-uitableviewcell-from-xib
How to do that? Just follow these easy steps
>##### 1. Add UITableView - remember add datasource and delegate 
>##### 2. Add custom cell - remember set Identifier value 
>##### 3. Populate data
```swift
class ViewController: UIViewController {
    let productCellId = "ProductTableViewCell"
    @IBOutlet weak var tableView: UITableView!
    var products = [ProductDto]()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view, typically from a nib.
        
        // Register cell
        tableView.register(UINib.init(nibName: productCellId, bundle: nil), forCellReuseIdentifier: productCellId)
        tableView.rowHeight = UITableViewAutomaticDimension
        tableView.separatorColor = UIColor.clear
        
        // Init data
        for _ in 1...25 {
            let product = ProductDto()
            product?.name = "Apple MacBook Air MC965LL/A 13.3"
            product?.desc = "The new MacBook Air is up to 2.5x faster than before. It features the latest Intel Core i5 dual-core processor, high-speed Thunderbolt I/O"
            products.append(product!)
        }
        tableView.reloadData()
    }
}
// ------------------------------------------------------------------------------
extension ViewController: UITableViewDelegate, UITableViewDataSource {
    func numberOfSections(in tableView: UITableView) -> Int {
        return 1
    }
    
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return products.count
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: productCellId, for: indexPath) as! ProductTableViewCell
        cell.selectionStyle = .none
        let product = products[indexPath.row]
        cell.lbName.text = product.name!
        cell.lbDesc.text = product.desc!
        return cell
    }
    
    func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        let product = products[indexPath.row]
        print("\(indexPath.row) - \(product.name!)")
    }
}
```

# Header-and-Footer-view-manage-in-collection-view

## Take a view controller with collection view
1. Take a CollectionReusableView Cocoa touch class with xib that is used for header and footer view.
2. Register the xib of CollectionReusableView class in collection view. 
    
    class ImgViewController: UIViewController {
    
     @IBOutlet weak var imgCollectionView: UICollectionView!
    
     var cellSpace = CGFloat(3)
     override func viewDidLoad() {
        super.viewDidLoad()
        
        imgCollectionView.register(UINib(nibName: "ImgCollectionViewCell", bundle: nil), forCellWithReuseIdentifier: "ImgCollectionViewCell")
        
        imgCollectionView.register(UINib(nibName: "MyCollectionReusableView", bundle: nil), forSupplementaryViewOfKind: UICollectionView.elementKindSectionHeader, withReuseIdentifier: "MyCollectionReusableView")
        
        imgCollectionView.register(UINib(nibName: "MyCollectionReusableView", bundle: nil), forSupplementaryViewOfKind: UICollectionView.elementKindSectionFooter, withReuseIdentifier: "MyCollectionReusableView")
        
        
        
        imgCollectionView.delegate = self
        imgCollectionView.dataSource = self
        
      }
    }

### Now use all datasource and delegate method


extension ImgViewController: UICollectionViewDelegate{
    
    
    
    func collectionView(_ collectionView: UICollectionView,
                        viewForSupplementaryElementOfKind kind: String,
                        at indexPath: IndexPath) -> UICollectionReusableView {
        
        switch kind {
        
        case UICollectionView.elementKindSectionHeader:
            let headerView = collectionView.dequeueReusableSupplementaryView(ofKind: kind, withReuseIdentifier: "MyCollectionReusableView", for: indexPath)
            headerView.layer.cornerRadius  = 25
            return headerView
            
        case UICollectionView.elementKindSectionFooter:
            let footerView = collectionView.dequeueReusableSupplementaryView(ofKind: kind, withReuseIdentifier: "MyCollectionReusableView", for: indexPath)
            
            return footerView
            
        default:
            assert(false, "Unexpected element kind")
        }
      }
    }
extension ImgViewController : UICollectionViewDataSource{
    
    func numberOfSections(in collectionView: UICollectionView) -> Int {
        return 3
    }
    func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
        return 30
    }
    
    func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        
        let cell = imgCollectionView.dequeueReusableCell(withReuseIdentifier: "ImgCollectionViewCell", for: indexPath) as! ImgCollectionViewCell
        
        return cell
      }
    }

extension ImgViewController : UICollectionViewDelegateFlowLayout{
    
    func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, sizeForItemAt indexPath: IndexPath) -> CGSize {
        
        let width  = Int(imgCollectionView.frame.size.width/4)-Int(cellSpace)
        
        return CGSize(width: width, height: width)
    }
    
    
    func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, referenceSizeForHeaderInSection section: Int) -> CGSize {
        return CGSize(width: collectionView.frame.width, height: 180.0)
        
        
    }
    func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, referenceSizeForFooterInSection section: Int) -> CGSize {
        return CGSize(width: 60.0, height: 0.0)
    }
    
    func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, minimumInteritemSpacingForSectionAt section: Int) -> CGFloat {
          return cellSpace
      }
      func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, minimumLineSpacingForSectionAt section: Int) -> CGFloat {
          return cellSpace
        }
      }

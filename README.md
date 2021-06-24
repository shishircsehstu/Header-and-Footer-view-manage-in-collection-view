# Header-and-Footer-view-manage-in-collection-view

### Take a view controller with collection view

import UIKit

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

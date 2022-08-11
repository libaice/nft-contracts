1. PUNK 上线的时候，当时Solidity 的版本才到了0.4，所以一些代码的风格于当前0.8版本代码的风格有点差异

2. Punk 在合约内部维护了一套买卖的流程。将手中的一份id 的Punk 进行挂单，使用

   ` function offerPunkForSale(uint punkIndex, uint minSalePriceInWei)`方法。里面会检查当前punk id 的owner是否为调用者，并在这个Map `punksOfferedForSale`中记录一份punk 挂单的详情。

   Offer 中包含五个字段

   ```
     struct Offer {
           bool isForSale;
           uint punkIndex;
           address seller;
           uint minValue;          // in ether
           address onlySellTo;     // specify to sell only to a specific person
       }
   ```

   

​	如果在挂单的时候，指定了onlySellTo的用户地址，那么只要这个地址的用户才能以minValue的价格来买下punk。 

​	在通过整个crpytoPunks市场的地板价格的时候，这些指定了最小价格的id, 需要被过滤出来的。
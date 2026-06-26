It is clearly Binary Search on Answers, Where we have to search mid (the accurate y, which separates the area between squares)

![[Pasted image 20260113180219.png]]

 ```cpp
 double separateSqaures(vector<vector<int>>& squares) {
	 double low = 1e18, high = -1e18;
	 
	 for(auto& s : squares) {
		 low = min(low, (double)s[1]);
		 high = max(high, (double)(s[1] + s[2]));
	 }
	 
	 for(int i=0; i<100; i++) {
		 double mid = (high + low) / 2.0;
		 double above = 0.0, below = 0.0;
		 
		 for(auto& s : squares) {
			 double y = s[1], l = s[2];
			 if(mid >= y + l) {
				 below += l * l;
			 }
			 else if(mid <= y){
				 above += l * l;
			 }
			 else {
				 below += l * (mid - y);
				 above += l * (y + l - mid);
			 }
		 }
		 
		 if(above > below) {
			 low = mid;
		 }
		 else {
			 high = mid;
		 }
	 }
	 
	 return low;
 }
 ```
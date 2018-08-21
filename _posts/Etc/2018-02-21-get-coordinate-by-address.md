---
layout: post
title:  "도로명 주소 기반으로 좌표값 얻어오기"
date:   2018-08-21
author: EunHye Jung
categories: etc
cover:  "/assets/instacode.png"
---  
     
     
### 도로명 주소 기반으로 좌표값 얻어오기     
    
     
* https://www.vworld.kr/v4po_svrint_a002.do API 이용   
  `API_KEY 발급받아야함`   
  
```python
import time
start_time = time.time()
        

coordinates = []
API_KEY = '발급받은 APIKEY'
for data in dataset.iterrows():
    res = requests.get('http://apis.vworld.kr/new2coord.do?q=' + data[1]['address'] + '&apiKey=' + API_KEY +'&domain=http://map.vworld.kr/&output=json').json()
    x = res.get('EPSG_4326_X')
    y = res.get('EPSG_4326_Y')
    if x is not None and y is not None:
        coordinate = [float(y),float(x)]  # folium에 이용하기 위해 실수값으로 변환
        coordinates.append(coordinate)
    else:
        coordinates.append([0.0, 0.0])
        
        
end_time = time.time()
print("실행 시간 : %s" %(end_time - start_time))
print(coordinates)
```     
   
   
   

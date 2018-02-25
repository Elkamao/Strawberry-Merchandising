##Table of Content
* [Project Background](#pro-back)
* [Strawberry Transactions](#straw-trans)
* [Promotion Analysis (Case Study)](#promo)
* [Market Busket Analsis](#mba)
* [Conclusion](#codebook)
* [Codebook](#codebook)


## <a name="pro-back"></a>Project Background
The aim of this project is to gain insights into grocery strawberry retail performance and provide  merchandising suggestions with data-supported evidences.

## <a name="straw-trans"></a>Strawberry Transactions
<img src="https://github.com/Elkamao/Strawberry-Merchandising/blob/master/Charts/Strawberry%20Sales%20by%20Month%20.png?raw=true" width="600">
 [code](#1-line-code)

<img src="https://github.com/Elkamao/Strawberry-Merchandising/blob/master/Charts/Strawberry%20Sales%20Decomposition.png?raw=true" width="600" >
 [code](#2-pie-code)


## <a name="promo"></a>Promotion Analysis (Case Study)

### 1. Promotion analysis

<img src="https://github.com/Elkamao/Strawberry-Merchandising/blob/master/Charts/Avg%20pct%20trans%20with%20promo%20by%20division.png?raw=true "width="600">
[code](#3-bar-code)

## <a name="mba"></a>Market Basket Analysis

## <a name="conclusion"></a>Conclusion

## <a name="codebook"></a>Codebook

### <a name="1-line-code"></a>Line Chart
```xml
<base table="certification.retail.salesdetail_customer"/>

<block name="sales_by_month_straw">
<note> Filter out Strawberries Transactions</note>
<link table2="certification.retail.products" col="sku" col2="sku"/>
<sel value="(groupdesc='FRUIT')"/>
<let search_string="STRAWBE">
  <sel value="(contains(description;{qv(@search_string)}))"/>
</let>

<willbe name="year" value="year(date)" label="Year" format="type:nocommas"/>
<willbe name="month" value="month(date)" label="Month"/>

<tabu label="Sales by Month" breaks="month" cbreaks="year">
  <tcol source="xsales" fun="sum" label="Total sale"/>
  <break col="month" sort="up"/>
  <break col="year" sort="up"/>
</tabu>
</block>

<note> Line chart for sales over months</note>

<dynamic>
  <widget class_="chart" type_="line" 
  base_="certification.retail.salesdetail_customer" width_="800" height_="600">
   <insert block="sales_by_month_straw"/>	
       <graphspec>
      <chartarea width="800" height="500"/>
      <title text="Strawberry Sales by Month (2011-2014)" font="20px sans-serif" color="black"/>
      <legend position="right">
        <labels font="15px sans-serif"/>
      </legend>
      </graphspec>   
  </widget>
</dynamic>
```
### <a name="2-pie-code"></a>Pie Chart
```xml
<base table="certification.retail.salesdetail_customer"/>
<block name="pct_promo_location">
<sel value="sku='322166'"/>
<sort col="promo" dir="up"/>
<willbe name="unit_promo" value="promo/qty" label="Unit Promo" format="dec:2"/>
<sort col="unit_promo" dir="up"/>
<willbe name="has_promo" value="if(promo<0;1;0)"/>
<willbe name="month" value="month(date)" label="Month"/>
<tabu label="Promotion by store" breaks="store" cbreaks="has_promo">
  <tcol fun="cnt" name="num_trans" source="transid" label="Number of Transaction" weight=""/>
</tabu>
<willbe name="pct_promo_trans" value="m0/num_trans*100" label="% Promoted Transaction"/>
<link table2="certification.retail.stores" col="store" col2="store" cols="divisiondesc,subdivisiondesc,city,state" shift="0"/>
<sort col="pct_promo_trans" dir="down"/>

<tabu label="Avg percent promotion by location" breaks="divisiondesc">
  <tcol source="pct_promo_trans" fun="avg" name="avg_pct_promo" label="Avg Percent of Transactions with Promotion"/>
</tabu>
</block>

<dynamic>
  <widget class_="chart" type_="bar" 
  base_="certification.retail.salesdetail_customer">
    <insert block="pct_promo_location"/>
     <graphspec>
      <title text="Avg Percent of Strawberry Transactions with Promotion by Division" 
       color="black" font="18px sans-serif">
      </title>
    </graphspec>
  </widget>
</dynamic>
```

### <a name="3-bar-code"></a>Bar Chart
```xml
<base table="certification.retail.salesdetail_customer"/>
<block name="pct_promo_location">
<sel value="sku='322166'"/>
<sort col="promo" dir="up"/>
<willbe name="unit_promo" value="promo/qty" label="Unit Promo" format="dec:2"/>
<sort col="unit_promo" dir="up"/>
<willbe name="has_promo" value="if(promo<0;1;0)"/>
<willbe name="month" value="month(date)" label="Month"/>
<tabu label="Promotion by store" breaks="store" cbreaks="has_promo">
  <tcol fun="cnt" name="num_trans" source="transid" label="Number of Transaction" weight=""/>
</tabu>
<willbe name="pct_promo_trans" value="m0/num_trans*100" label="% Promoted Transaction"/>
<link table2="certification.retail.stores" col="store" col2="store" cols="divisiondesc,subdivisiondesc,city,state" shift="0"/>
<sort col="pct_promo_trans" dir="down"/>

<tabu label="Avg percent promotion by location" breaks="divisiondesc">
  <tcol source="pct_promo_trans" fun="avg" name="avg_pct_promo" label="Avg Percent of Transactions with Promotion"/>
</tabu>
</block>

<dynamic>
  <widget class_="chart" type_="bar" 
  base_="certification.retail.salesdetail_customer">
    <insert block="pct_promo_location"/>
     <graphspec>
      <title text="Avg Percent of Strawberry Transactions with Promotion by Division" 
       color="black" font="18px sans-serif">
      </title>
    </graphspec>
  </widget>
</dynamic>
```



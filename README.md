# Splunk4Rookies - Hands On Workshop

## Introduction

Today, Splunk presented a workshop to the public, highlighting the power of their platform with key SPL (Search Processing Language) searches. The session showcased several key searches:

1. **Customer Locations Search:** Identified customer IPs and geolocated them to cities outside the United States.
2. **Lost Revenue Search:** Calculated lost revenue from failed purchase attempts.
3. **Web Browser Failures Search:** Counted and charted web browsers with the most access failures.
4. **Popular Operating Systems Search:** Listed the top 10 operating systems from access logs.
5. **Web Server Status Codes Search:** Tracked web server status codes over time.

These examples provided just a glimpse of what Splunk has to offer, demonstrating how it can turn data into valuable insights for enhanced decision-making and operational efficiency.

## Resources

Splunk lab was provided for this workshop. However, if you are interested in deploying your own community version of Splunk on AWS, please follow my Splunk on AWS walkthrough. 

Below are a few resources I'll be using to help supplement my journey to learn Splunk!

**Splunk Links**
 - [Splunk SPL Search Reference](https://docs.splunk.com/Documentation/SplunkCloud/latest/SearchReference/ListOfSearchCommand)
 - [Splunkbase](https://splunkbase.splunk.com/)

**Books**
 - [Practical Splunk Search Processing Language](https://www.amazon.com/Practical-Splunk-Search-Processing-Language/dp/1484262751/ref=sr_1_1?crid=9MOUW1AETJXZ&dib=eyJ2IjoiMSJ9.fD8M2q9hz-6D6Ff7o6J3PJYkzspzU1R4BsmkR-VCl_Czg2fS0hJRRqa8TKv6V6mG.VXyUVRz5wixR7P6Uq5us29-1zqT8KmUTM1imD0is8vs&dib_tag=se&keywords=Practical+Splunk+Search+Processing+Language&qid=1721344923&sprefix=practical+splunk+search+processing+language%2Caps%2C110&sr=8-1)
- [Mastering Splunk: A Comprehesive Guide for Beginners](https://www.amazon.com/Mastering-Splunk-Comprehensive-Architecture-Visualization/dp/B0CWMXMS5G/ref=sr_1_1?crid=QZJL5UXL9GN1&dib=eyJ2IjoiMSJ9.C4rlyfyeFN-dD2yVbW1pt3beVcRsQch51xW8G75MezgFlnXLoCMWWD-wV4HnYCg_4mDhtCL-DY1ezVAbjwsxV69xaCr9-LuoH08y-T5Wf43YuMiO2JBVix2DYoAOXgjW.A2YLU1VRHIB2wUp3G84h8ajuJbELFEctRFmp8qBThe8&dib_tag=se&keywords=Mastering+Splunk&qid=1721345079&sprefix=mastering+splunk%2Caps%2C117&sr=8-1)

## SPL to Dashboard

Visualizations come to life from saved SPL searches in Splunk, turning raw data into interactive, insightful visuals. This makes it easier to identify patterns, trends, and anomalies, allowing organizations to monitor key metrics and make informed decisions swiftly. Splunk's dynamic visual tools enhance data analysis and support a data-driven approach.

Below are the saved searches that made the Buttercup Enterprises Dashboard come true.

**Business Analytics**

index=main sourcetype="access_combined" action=purchase status>=400
| lookup product_codes.csv product_id
| timechart sum(product_price)

**IT Ops - Web Server Status Codes Over Time**

index=main sourcetype="access_combined"| timechart count by status limit=10

**DevOps - Most Popular Operating Systems**

index=_* OR index=* sourcetype=access_combined| top limit=20 platforms showperc=f

**DevOps - Web Browser With Most Failures**  

index=main sourcetype="access_combined" status>=400| timechart count by useragent limit=5  useother=f

**Security and Fraud - Customer Locations**

index=mainsourcetype=access_combined | iplocation clientip | search Country!="UnitedStates" | geostats count by City

## Conclusion
Attending the Splunk workshop was a fantastic experience for me. I gained valuable insights into creating effective visualizations and understanding their impact on data analysis. The hands-on sessions were particularly useful, allowing me to apply what I learned in real time. Overall, it was a great opportunity to enhance my skills and knowledge in using Splunk for data analysis. Check my Splunk dashboard below!

![Splunk4Rookies - Dashboard](https://github.com/createdbymp/splunk4rookies-workshop/issues)

 

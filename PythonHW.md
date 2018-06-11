# HW
Python
import pandas as pd
data = pd.read_csv('Energy_and_Water_Use_-_Municipal_Buildings.csv')

#1.energy_star_score>=75(ค่าคะแนนการประหยัดพลังงาน 75-100คะแนนถือว่าดีมาก)
data.iloc[:,[0,7,8,3]][(data['energy_star_score '] >=75)].sort_values(by='energy_star_score ',ascending=0)

#2.poproty name  top 5  total emission metric (หน่วยงานใดมีการปล่อยมลพิษรวมสูงสุด 5 อันดับ)
data['total_ghg_emissions_metric_tons_co2e'].groupby(data['department']).describe()

#3.	average total emission metric(ค่าเฉลี่ยของการปล่อยมลพิษในแต่ละแห่งแต่ละปี)
data['total_ghg_emissions_metric_tons_co2e'].groupby(data['department']).describe()

#4.	average of total emission intensity of each department
data['total_ghg_emissions_intensity_kgco2e_ft'].groupby(data['department']).describe()

#5.	max property_gfa (หน่วยงานใดมีพื้นที่สูงสุด)
data.iloc[:,[1,8,7,4]][(data['property_gfa___self_reported_ft']==data.property_gfa___self_reported_ft.idxmax()) | (data['property_gfa___self_reported_ft'] ==data.property_gfa___self_reported_ft.max())]	

#6.	count each kind of department (มีหน่วยงานแบบไหนบ้าง จำนวนเท่าไร)
data['department'].groupby(data['department']).describe()

#7.	water_use_all_water_sources_kgal=0(หน่วยงานที่ไม่มีการใช้น้ำเลย)
data.iloc[:,[0,7,8]][(data['water_use_all_water_sources_kgal'] ==0)]

#8.	max water_use_all_water_sources_kgal in 2015 (หน่วยงานที่ใช้น้ำในปี2015มากที่สุด)
data.groupby(['year_ending'])['water_use_all_water_sources_kgal'].max()

#9.	weather_normalized = 0 (ที่สภาพอากาศปกติมี ค่าEUI(Energy Utilization Index)=0)
data.iloc[:,[0,7,8]][(data['weather_normalized_site_eui_kbtu_ft'] ==0)]

#10.	source-site ratios (แสดงว่ามีการสูญเสียทางการขนส่งน้ำ สมมติว่า>0.45ถือว่าดี)
data['EffTrans'] = data['weather_normalized_site_eui_kbtu_ft']/data['weather_normalized_source_eui_kbtu_ft']
data.iloc[:,[0,7,8,15,14,19]][(data['weather_normalized_site_eui_kbtu_ft'] >0)]


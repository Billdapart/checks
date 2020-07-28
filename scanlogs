#!/usr/bin/env python3

import re, operator, os, csv

error_inst = {}
user_inst = {}

error_ptn = r'ticky: ERROR ([\w\s\']*) \((.+)\)'
info_ptn = r'ticky: INFO.* \((.+)\)'

with open('syslog.log','r') as logs:
  for line in logs.readlines():
    if re.search(error_ptn,line):
      extracts = re.search(error_ptn, line)
      error_inst.setdefault(extracts.group(1),0)
      error_inst[extracts.group(1)]+=1
      user_inst.setdefault(extracts.group(2),[0,0])[1]+=1
    if re.search(info_ptn,line):
      extracts = re.search(info_ptn, line)
      user_inst.setdefault(extracts.group(1),[0,0])[0]+=1

error_sort = sorted(error_inst.items(), key = operator.itemgetter(1), reverse = True)
user_sort = sorted(user_inst.items())
print(error_sort)
print(user_sort)

with open('error_message.csv','w') as output:
  writer = csv.writer(output)
  writer.writerow(['Error','Count'])
  writer.writerows(error_sort)

with open('user_statistics.csv','w') as output:
  writer = csv.writer(output)
  writer.writerow(['Username','INFO','ERROR'])
  for item in user_sort:
      onerow = [item[0],item[1][0],item[1][1]]
      writer.writerow(onerow)

# mis
管理信息系统作业

数据库建立

DROP TABLE IF EXISTS `保养信息表`;

CREATE TABLE `保养信息表` (

`保养ID` int(20) NOT NULL,

`外保养类别` varchar(50) NOT NULL,

`保养人` varchar(255) NOT NULL,

`班组` varchar(255) NOT NULL,

PRIMARY KEY (`保养ID`),

KEY `保养类别` (`外保养类别`)

) ENGINE=InnoDB DEFAULT CHARSET=utf8;

INSERT INTO `保养信息表` VALUES ('1', '月检', '李四', '1组');

DROP TABLE IF EXISTS `保养记录表`;

CREATE TABLE `保养记录表` (

  `保养记录ID` int(20) NOT NULL AUTO_INCREMENT,
  
  `外设备ID` int(20) NOT NULL,
  
  `外保养ID` int(20) NOT NULL,
  
  `保养时间` date NOT NULL,

  `说明` varchar(255) DEFAULT NULL,
  
  `外消耗ID` int(20) DEFAULT NULL,
  
  PRIMARY KEY (`保养记录ID`),
  
  KEY `设备ID` (`外设备ID`),
  
  KEY `保养ID` (`外保养ID`),
  
  KEY `消耗ID` (`外消耗ID`),
  
  CONSTRAINT `保养ID` FOREIGN KEY (`外保养ID`) REFERENCES `保养信息` (`保养ID`),
  
  CONSTRAINT `消耗ID` FOREIGN KEY (`外消耗ID`) REFERENCES `消耗记录` (`消耗ID`),
  
  CONSTRAINT `设备ID` FOREIGN KEY (`外设备ID`) REFERENCES `设备信息` (`设备ID`)
  
) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8;

INSERT INTO `保养记录表` VALUES ('1', '123456', '1', '2016-09-14', null, '1');

DROP TABLE IF EXISTS `检修情况表`;

CREATE TABLE `检修情况表` (

  `ID` int(20) NOT NULL AUTO_INCREMENT,
  
  `保养内容` varchar(255) NOT NULL,
  
  `完成状况` varchar(255) NOT NULL,
  
  `备注` varchar(255) DEFAULT NULL,
  
  `检修设备ID` int(20) NOT NULL,
  
  PRIMARY KEY (`ID`),
  
  KEY `检修设备ID` (`检修设备ID`),
  
  CONSTRAINT `检修设备ID` FOREIGN KEY (`检修设备ID`) REFERENCES `设备信息` (`设备ID`)
  
) ENGINE=InnoDB AUTO_INCREMENT=8 DEFAULT CHARSET=utf8;


INSERT INTO `检修情况表` VALUES ('1', '检查接线紧固情况和电缆磨损情况', '完成', null, '123456');

INSERT INTO `检修情况表` VALUES ('2', '检查液位仪传感器周围漏液和磨损情况', '完成', '更换传感器', '123456');


INSERT INTO `检修情况表` VALUES ('3', '校对液位仪准确度', '完成', null, '123456');

DROP TABLE IF EXISTS `检修项目表`;

CREATE TABLE `检修项目表` (

  `设备类别` varchar(50) NOT NULL,
  
  `保养类别` varchar(50) NOT NULL,
  

`保养内容` varchar(255) NOT NULL,
  
  KEY `保养类别` (`保养类别`),
  
  KEY `设备类别` (`设备类别`),  
  CONSTRAINT `保养类别` FOREIGN KEY (`保养类别`) REFERENCES `保养信息` (`外保养类别`),
  
  CONSTRAINT `设备类别` FOREIGN KEY (`设备类别`) REFERENCES `设备信息` (`外设备类别`)
  
) ENGINE=InnoDB DEFAULT CHARSET=utf8;


INSERT INTO `检修项目表` VALUES ('液位仪', '月检', '检查接线紧固情况和电缆磨损情况');


INSERT INTO `检修项目表` VALUES ('液位仪', '月检', '检查液位仪传感器周围漏液和磨损情况');
INSERT INTO `检修项目表` VALUES ('液位仪', '月检', '校对液位仪准确度');

DROP TABLE IF EXISTS `消耗记录表`;

CREATE TABLE `消耗记录表` (

  `消耗ID` int(20) NOT NULL,
  
  `修理内容` varchar(255) NOT NULL,
  
  `消耗材料` varchar(255) NOT NULL,
  
  `消耗数量` int(20) NOT NULL,
  
  `剩余数量` int(20) NOT NULL,
  
  KEY `消耗ID` (`消耗ID`)
  
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

INSERT INTO `消耗记录表` VALUES ('1', '更换传感器', '传感器', '1', '9');

DROP TABLE IF EXISTS `设备信息表`;

CREATE TABLE `设备信息表` (

  `设备ID` int(20) NOT NULL,
  
  `外设备类别` varchar(50) NOT NULL,
  
  `最新一次维修时间` varchar(50) NOT NULL,
  
  PRIMARY KEY (`设备ID`),
  
  KEY `设备类型` (`外设备类别`)
  
) ENGINE=InnoDB DEFAULT CHARSET=utf8;

INSERT INTO `设备信息表` VALUES ('123456', '液位仪', '2016-08-10');

设备保养情况查询截图：

![](/查询图1.png)
![](/查询图2.png)
![](/查询图3.png)

ER图截图：

![](/ER截图.png)

axure原型设计发布链接：http://9f1w0d.axshare.com

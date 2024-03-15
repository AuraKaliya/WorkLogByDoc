## 目标

1. 点阵有序排列
2. 找出点链接的单元



## 输入数据

* 焊线点列表
* 几何体单元统计表
* 点对应空间位置表
* 几何体单元所含点阵表
* 初始点、初始单元、初始法线

```c++
    //焊线点列表
	QSet<int> m_myPointIDSet;   
	//几何体单元统计表
    QSet<int> m_unitIDSet;		
	//点对应空间位置表
    QMap<int,QVector<double> > m_pointPosDictionary;
	//几何体单元所含点阵表			
    QMap<int,QSet<int>> m_geoDictionary;	

	//初始点、初始单元、初始法线
    int m_startPointID;
    int m_startUnitID;
    Eigen::Vector3d m_startNormalVector;
```

## 输出数据

* 点阵序列表
* 点链接单元表

```c++
    //点阵序列表
    QVector<QVector<int> > m_finalPointIDList;
	//点链接单元表
    QMap<int,QSet<int> > m_pointToUnitDictionary;
```

## 一些临时变量

* 下一列点表
* 下一列起始单元备选表
* 控制位

```
    QVector<int> m_nextPointIDList;
    QVector<int> m_spareNextUnitList;
    
    bool m_finished;
    bool m_colTailFlag;
    bool m_rowTailFlag;
    bool m_rowHeadFlag;
```



## 步骤

### 找点链接单元

遍历m_geoDictionary，对每个单元所含的每个点，把这个单元加入到m_pointToUnitDictionary的该点对应的集合中。

### 点阵有序化

由左到右，由上到下，针对每个层进行操作。

由控制位进行逻辑转换判断。

对每个层：

1. 预处理部分

2. 找到焊线向量

3. 找到当前面的下一层目标点列表

4. 找到下一层起始单元

    ```c++
    void GeObject::solveUnit(int startPointID, int startUnitID, Eigen::Vector3d normalVector, int wireBondingPointID)
    ```

备注：

* wireBondingPointID=0时，表示是第一列第一行处理，需要从焊线点表中找到焊线点
* 找目标点时需要判断是上三角、下三角还是四边形，通过与焊线向量的夹角区分now和next


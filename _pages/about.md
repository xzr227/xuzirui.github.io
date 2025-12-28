---
permalink: /
title: "Academic Pages is a ready-to-fork GitHub Pages template for academic personal websites"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>短途电动货车月度成本测算程序</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
        }
        
        body {
            background-color: #f5f7fa;
            color: #333;
            line-height: 1.6;
            padding: 20px;
            max-width: 1200px;
            margin: 0 auto;
        }
        
        .container {
            display: flex;
            flex-direction: column;
            gap: 25px;
        }
        
        header {
            text-align: center;
            padding: 20px;
            background: linear-gradient(135deg, #2c3e50, #4a6491);
            color: white;
            border-radius: 10px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
        }
        
        h1 {
            font-size: 2.2rem;
            margin-bottom: 10px;
        }
        
        .subtitle {
            font-size: 1.1rem;
            opacity: 0.9;
        }
        
        .content {
            display: flex;
            flex-wrap: wrap;
            gap: 25px;
        }
        
        .input-section, .results-section {
            flex: 1;
            min-width: 300px;
            background-color: white;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
        }
        
        .section-title {
            font-size: 1.4rem;
            color: #2c3e50;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid #3498db;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #444;
        }
        
        input, select {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 6px;
            font-size: 1rem;
            transition: border 0.3s;
        }
        
        input:focus, select:focus {
            border-color: #3498db;
            outline: none;
            box-shadow: 0 0 0 2px rgba(52, 152, 219, 0.2);
        }
        
        .unit {
            color: #7f8c8d;
            font-size: 0.9rem;
            margin-left: 5px;
        }
        
        .btn-calculate {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 15px 30px;
            font-size: 1.1rem;
            border-radius: 6px;
            cursor: pointer;
            width: 100%;
            transition: background-color 0.3s;
            font-weight: 600;
            margin-top: 10px;
        }
        
        .btn-calculate:hover {
            background-color: #2980b9;
        }
        
        .cost-item {
            display: flex;
            justify-content: space-between;
            margin-bottom: 15px;
            padding-bottom: 15px;
            border-bottom: 1px dashed #eee;
        }
        
        .cost-name {
            font-weight: 500;
        }
        
        .cost-value {
            font-weight: 600;
            color: #2c3e50;
        }
        
        .highlight {
            background-color: #f8f9fa;
            padding: 15px;
            border-radius: 8px;
            margin-top: 10px;
            border-left: 4px solid #3498db;
        }
        
        .total-cost {
            font-size: 1.8rem;
            color: #e74c3c;
            text-align: center;
            margin: 20px 0;
        }
        
        .unit-cost {
            font-size: 1.4rem;
            color: #27ae60;
            text-align: center;
            margin: 20px 0;
        }
        
        .charts-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .chart-box {
            background-color: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
        }
        
        .chart-title {
            font-size: 1.2rem;
            color: #2c3e50;
            margin-bottom: 15px;
            text-align: center;
        }
        
        .explanation {
            background-color: #f9f9f9;
            padding: 20px;
            border-radius: 8px;
            margin-top: 20px;
            font-size: 0.95rem;
            line-height: 1.7;
        }
        
        .explanation h3 {
            color: #2c3e50;
            margin-bottom: 10px;
        }
        
        @media (max-width: 768px) {
            .content {
                flex-direction: column;
            }
            
            h1 {
                font-size: 1.8rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>短途电动货车月度成本测算程序</h1>
            <p class="subtitle">基于电动货车特性，测算月度固定成本、变动成本、总成本及单位成本（平均装载率75%）</p>
        </header>
        
        <div class="content">
            <div class="input-section">
                <h2 class="section-title">基础数据输入</h2>
                
                <div class="form-group">
                    <label>月均行驶趟数 <span class="unit">(趟)</span></label>
                    <input type="number" id="monthlyTrips" value="20" min="1" max="100">
                </div>
                
                <div class="form-group">
                    <label>单程平均距离 <span class="unit">(公里)</span></label>
                    <input type="number" id="tripDistance" value="80" min="1" max="100">
                </div>
                
                <div class="form-group">
                    <label>车辆载重能力 <span class="unit">(吨)</span></label>
                    <input type="number" id="vehicleCapacity" value="4.5" min="1" max="10" step="0.1">
                </div>
                
                <div class="form-group">
                    <label>平均装载率 <span class="unit">(%)</span></label>
                    <input type="number" id="loadRate" value="75" min="1" max="100">
                    <small style="color:#7f8c8d; display:block; margin-top:5px;">用于计算单位吨公里成本</small>
                </div>
                
                <h3 class="section-title">固定成本参数</h3>
                
                <div class="form-group">
                    <label>司机月工资 <span class="unit">(元/月)</span></label>
                    <input type="number" id="driverSalary" value="6000" min="0">
                </div>
                
                <div class="form-group">
                    <label>车辆购置成本 <span class="unit">(万元)</span></label>
                    <input type="number" id="vehicleCost" value="18" min="0" step="0.1">
                </div>
                
                <div class="form-group">
                    <label>车辆折旧年限 <span class="unit">(年)</span></label>
                    <input type="number" id="depreciationYears" value="5" min="1" max="10">
                </div>
                
                <div class="form-group">
                    <label>保险费用 <span class="unit">(元/年)</span></label>
                    <input type="number" id="insurance" value="8000" min="0">
                </div>
                
                <div class="form-group">
                    <label>年检费用 <span class="unit">(元/年)</span></label>
                    <input type="number" id="inspectionFee" value="1000" min="0">
                </div>
                
                <h3 class="section-title">变动成本参数</h3>
                
                <div class="form-group">
                    <label>电耗率 <span class="unit">(千瓦时/百公里)</span></label>
                    <input type="number" id="energyConsumption" value="40" min="1">
                </div>
                
                <div class="form-group">
                    <label>电价 <span class="unit">(元/千瓦时)</span></label>
                    <input type="number" id="electricityPrice" value="1.2" min="0" step="0.01">
                </div>
                
                <div class="form-group">
                    <label>路桥费 <span class="unit">(元/公里)</span></label>
                    <input type="number" id="tollFee" value="0.8" min="0" step="0.01">
                </div>
                
                <div class="form-group">
                    <label>维修保养费 <span class="unit">(元/公里)</span></label>
                    <input type="number" id="maintenanceCost" value="0.15" min="0" step="0.01">
                </div>
                
                <div class="form-group">
                    <label>轮胎更换成本 <span class="unit">(元/万公里)</span></label>
                    <input type="number" id="tireCost" value="800" min="0">
                </div>
                
                <button class="btn-calculate" onclick="calculateCosts()">测算成本</button>
            </div>
            
            <div class="results-section">
                <h2 class="section-title">月度成本测算结果</h2>
                
                <div class="cost-breakdown">
                    <h3 style="color: #3498db; margin-bottom: 15px;">固定成本 (元/月)</h3>
                    
                    <div class="cost-item">
                        <span class="cost-name">司机工资</span>
                        <span class="cost-value" id="driverSalaryCost">0</span>
                    </div>
                    
                    <div class="cost-item">
                        <span class="cost-name">车辆折旧</span>
                        <span class="cost-value" id="depreciationCost">0</span>
                    </div>
                    
                    <div class="cost-item">
                        <span class="cost-name">保险费用</span>
                        <span class="cost-value" id="insuranceCost">0</span>
                    </div>
                    
                    <div class="cost-item">
                        <span class="cost-name">年检费用</span>
                        <span class="cost-value" id="inspectionCost">0</span>
                    </div>
                    
                    <div class="highlight">
                        <div class="cost-item">
                            <span class="cost-name">月度固定成本合计</span>
                            <span class="cost-value" id="totalFixedCost">0</span>
                        </div>
                    </div>
                    
                    <h3 style="color: #3498db; margin: 25px 0 15px 0;">变动成本 (元/月)</h3>
                    
                    <div class="cost-item">
                        <span class="cost-name">电费成本</span>
                        <span class="cost-value" id="energyCost">0</span>
                    </div>
                    
                    <div class="cost-item">
                        <span class="cost-name">路桥费</span>
                        <span class="cost-value" id="tollCost">0</span>
                    </div>
                    
                    <div class="cost-item">
                        <span class="cost-name">维修保养费</span>
                        <span class="cost-value" id="maintenanceTotal">0</span>
                    </div>
                    
                    <div class="cost-item">
                        <span class="cost-name">轮胎更换成本</span>
                        <span class="cost-value" id="tireTotal">0</span>
                    </div>
                    
                    <div class="highlight">
                        <div class="cost-item">
                            <span class="cost-name">月度变动成本合计</span>
                            <span class="cost-value" id="totalVariableCost">0</span>
                        </div>
                    </div>
                    
                    <div class="total-cost">
                        月度总成本: <span id="totalMonthlyCost">0</span> 元
                    </div>
                    
                    <div class="unit-cost">
                        单位成本 (吨·公里): <span id="unitCost">0</span> 元
                    </div>
                </div>
                
                <div class="charts-container">
                    <div class="chart-box">
                        <div class="chart-title">成本结构分析</div>
                        <canvas id="costStructureChart"></canvas>
                    </div>
                    
                    <div class="chart-box">
                        <div class="chart-title">固定成本 vs 变动成本</div>
                        <canvas id="fixedVariableChart"></canvas>
                    </div>
                </div>
                
                <div class="explanation">
                    <h3>测算说明</h3>
                    <p>1. 本测算基于电动货车在短途运输场景（单程100公里以内）设计。</p>
                    <p>2. 固定成本：与行驶里程无关的月度固定支出，包括司机工资、车辆折旧、保险、年检等。</p>
                    <p>3. 变动成本：与行驶里程相关的支出，包括电费、路桥费、维修保养、轮胎磨损等。</p>
                    <p>4. 单位成本计算：基于平均装载率(75%)计算每吨公里的运输成本，公式为：总成本 ÷ (总吨公里数)。</p>
                    <p>5. 总吨公里数 = 月均趟数 × 单程距离 × 2（往返） × 车辆载重 × 平均装载率。</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        // 初始化变量
        let costStructureChart, fixedVariableChart;
        
        // 页面加载完成后初始化图表
        window.onload = function() {
            initializeCharts();
            calculateCosts(); // 初始计算一次
        };
        
        // 初始化图表
        function initializeCharts() {
            const ctx1 = document.getElementById('costStructureChart').getContext('2d');
            const ctx2 = document.getElementById('fixedVariableChart').getContext('2d');
            
            // 销毁之前的图表实例
            if (costStructureChart) costStructureChart.destroy();
            if (fixedVariableChart) fixedVariableChart.destroy();
            
            // 成本结构图表
            costStructureChart = new Chart(ctx1, {
                type: 'pie',
                data: {
                    labels: ['司机工资', '车辆折旧', '保险费用', '年检费用', '电费成本', '路桥费', '维修保养', '轮胎成本'],
                    datasets: [{
                        data: [0, 0, 0, 0, 0, 0, 0, 0],
                        backgroundColor: [
                            '#3498db', '#2ecc71', '#e74c3c', '#f39c12',
                            '#9b59b6', '#1abc9c', '#d35400', '#34495e'
                        ],
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    plugins: {
                        legend: {
                            position: 'bottom',
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    const label = context.label || '';
                                    const value = context.raw || 0;
                                    const total = context.dataset.data.reduce((a, b) => a + b, 0);
                                    const percentage = total > 0 ? Math.round((value / total) * 100) : 0;
                                    return `${label}: ${value.toFixed(2)}元 (${percentage}%)`;
                                }
                            }
                        }
                    }
                }
            });
            
            // 固定成本 vs 变动成本图表
            fixedVariableChart = new Chart(ctx2, {
                type: 'doughnut',
                data: {
                    labels: ['固定成本', '变动成本'],
                    datasets: [{
                        data: [0, 0],
                        backgroundColor: ['#3498db', '#2ecc71'],
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    plugins: {
                        legend: {
                            position: 'bottom',
                        }
                    }
                }
            });
        }
        
        // 计算成本函数
        function calculateCosts() {
            // 获取输入值
            const monthlyTrips = parseFloat(document.getElementById('monthlyTrips').value);
            const tripDistance = parseFloat(document.getElementById('tripDistance').value);
            const vehicleCapacity = parseFloat(document.getElementById('vehicleCapacity').value);
            const loadRate = parseFloat(document.getElementById('loadRate').value) / 100;
            
            // 固定成本参数
            const driverSalary = parseFloat(document.getElementById('driverSalary').value);
            const vehicleCost = parseFloat(document.getElementById('vehicleCost').value) * 10000; // 转换为元
            const depreciationYears = parseFloat(document.getElementById('depreciationYears').value);
            const insurance = parseFloat(document.getElementById('insurance').value);
            const inspectionFee = parseFloat(document.getElementById('inspectionFee').value);
            
            // 变动成本参数
            const energyConsumption = parseFloat(document.getElementById('energyConsumption').value);
            const electricityPrice = parseFloat(document.getElementById('electricityPrice').value);
            const tollFee = parseFloat(document.getElementById('tollFee').value);
            const maintenanceCost = parseFloat(document.getElementById('maintenanceCost').value);
            const tireCost = parseFloat(document.getElementById('tireCost').value);
            
            // 计算月度总里程 (往返)
            const monthlyDistance = monthlyTrips * tripDistance * 2; // 往返
            
            // 计算固定成本 (月度)
            const driverSalaryCost = driverSalary;
            const depreciationCost = vehicleCost / (depreciationYears * 12);
            const insuranceCost = insurance / 12;
            const inspectionCost = inspectionFee / 12;
            
            const totalFixedCost = driverSalaryCost + depreciationCost + insuranceCost + inspectionCost;
            
            // 计算变动成本 (月度)
            const energyCost = (monthlyDistance / 100) * energyConsumption * electricityPrice;
            const tollCost = monthlyDistance * tollFee;
            const maintenanceTotal = monthlyDistance * maintenanceCost;
            const tireTotal = (monthlyDistance / 10000) * tireCost;
            
            const totalVariableCost = energyCost + tollCost + maintenanceTotal + tireTotal;
            
            // 计算总成本
            const totalMonthlyCost = totalFixedCost + totalVariableCost;
            
            // 计算单位成本 (吨公里成本)
            // 总吨公里 = 月均趟数 × 单程距离 × 2（往返） × 车辆载重 × 平均装载率
            const totalTonKm = monthlyTrips * tripDistance * 2 * vehicleCapacity * loadRate;
            const unitCost = totalTonKm > 0 ? totalMonthlyCost / totalTonKm : 0;
            
            // 更新显示结果
            document.getElementById('driverSalaryCost').textContent = driverSalaryCost.toFixed(2);
            document.getElementById('depreciationCost').textContent = depreciationCost.toFixed(2);
            document.getElementById('insuranceCost').textContent = insuranceCost.toFixed(2);
            document.getElementById('inspectionCost').textContent = inspectionCost.toFixed(2);
            document.getElementById('totalFixedCost').textContent = totalFixedCost.toFixed(2);
            
            document.getElementById('energyCost').textContent = energyCost.toFixed(2);
            document.getElementById('tollCost').textContent = tollCost.toFixed(2);
            document.getElementById('maintenanceTotal').textContent = maintenanceTotal.toFixed(2);
            document.getElementById('tireTotal').textContent = tireTotal.toFixed(2);
            document.getElementById('totalVariableCost').textContent = totalVariableCost.toFixed(2);
            
            document.getElementById('totalMonthlyCost').textContent = totalMonthlyCost.toFixed(2);
            document.getElementById('unitCost').textContent = unitCost.toFixed(4);
            
            // 更新图表数据
            updateCharts(
                [driverSalaryCost, depreciationCost, insuranceCost, inspectionCost, 
                 energyCost, tollCost, maintenanceTotal, tireTotal],
                [totalFixedCost, totalVariableCost]
            );
        }
        
        // 更新图表数据
        function updateCharts(costStructureData, fixedVariableData) {
            // 更新成本结构图表
            costStructureChart.data.datasets[0].data = costStructureData;
            costStructureChart.update();
            
            // 更新固定成本 vs 变动成本图表
            fixedVariableChart.data.datasets[0].data = fixedVariableData;
            fixedVariableChart.update();
        }
        
        // 为所有输入框添加事件监听，实现实时计算
        document.querySelectorAll('input').forEach(input => {
            input.addEventListener('input', calculateCosts);
        });
    </script>
</body>
</html>


# Customer-Sales-Analysis-Interactive-Reporting-Dashboard
import React, { useState } from 'react';

const PowerBIDashboard = () => {
  const [activeTab, setActiveTab] = useState('overview');
  
  // Sample data
  const quarterlyData = [
    { quarter: 'Q1-2024', sales: 1245000, customers: 3280, avgOrder: 379.57 },
    { quarter: 'Q2-2024', sales: 1587000, customers: 3860, avgOrder: 411.14 },
    { quarter: 'Q3-2024', sales: 1358000, customers: 3520, avgOrder: 385.80 },
    { quarter: 'Q4-2024', sales: 1763000, customers: 4120, avgOrder: 427.91 }
  ];
  
  const segmentData = [
    { segment: 'Champions', count: 842, percentage: 28, avgSpend: 1250, retention: 92 },
    { segment: 'Potential Loyalists', count: 1265, percentage: 42, avgSpend: 850, retention: 78 },
    { segment: 'At Risk', count: 625, percentage: 21, avgSpend: 480, retention: 45 },
    { segment: 'Needs Attention', count: 268, percentage: 9, avgSpend: 220, retention: 23 }
  ];
  
  const productData = [
    { category: 'Electronics', sales: 985000, growth: 15.2, margin: 32, units: 12450 },
    { category: 'Home Goods', sales: 645000, growth: 8.7, margin: 38, units: 28300 },
    { category: 'Fashion', sales: 825000, growth: 11.5, margin: 42, units: 31200 },
    { category: 'Health & Beauty', sales: 542000, growth: 18.3, margin: 46, units: 24800 }
  ];

  const formatCurrency = (value) => {
    return new Intl.NumberFormat('en-US', {
      style: 'currency',
      currency: 'USD',
      minimumFractionDigits: 0,
      maximumFractionDigits: 0
    }).format(value);
  };

  return (
    <div className="w-full max-w-6xl mx-auto bg-gray-50 p-4 rounded-lg shadow">
      <div className="bg-white p-4 rounded-lg shadow mb-6">
        <h1 className="text-2xl font-bold text-gray-800 mb-2">Customer Sales Analysis Dashboard</h1>
        <p className="text-gray-600">Interactive visualization of customer segmentation and sales performance</p>
      </div>

      {/* Navigation Tabs */}
      <div className="flex mb-6 bg-white rounded-lg shadow overflow-hidden">
        <button 
          className={`px-4 py-3 font-medium ${activeTab === 'overview' ? 'bg-blue-600 text-white' : 'text-gray-700 hover:bg-gray-100'}`}
          onClick={() => setActiveTab('overview')}
        >
          Sales Overview
        </button>
        <button 
          className={`px-4 py-3 font-medium ${activeTab === 'segments' ? 'bg-blue-600 text-white' : 'text-gray-700 hover:bg-gray-100'}`}
          onClick={() => setActiveTab('segments')}
        >
          Customer Segments
        </button>
        <button 
          className={`px-4 py-3 font-medium ${activeTab === 'products' ? 'bg-blue-600 text-white' : 'text-gray-700 hover:bg-gray-100'}`}
          onClick={() => setActiveTab('products')}
        >
          Product Performance
        </button>
      </div>

      {/* Content based on active tab */}
      {activeTab === 'overview' && (
        <div className="space-y-6">
          {/* KPI Cards */}
          <div className="grid grid-cols-1 md:grid-cols-4 gap-4">
            <div className="bg-white p-4 rounded-lg shadow">
              <h3 className="text-gray-500 text-sm">Total Sales (YTD)</h3>
              <p className="text-2xl font-bold text-gray-800">{formatCurrency(5953000)}</p>
              <p className="text-green-600 text-sm">↑ 12.8% vs Previous Year</p>
            </div>
            <div className="bg-white p-4 rounded-lg shadow">
              <h3 className="text-gray-500 text-sm">Total Customers</h3>
              <p className="text-2xl font-bold text-gray-800">3,000</p>
              <p className="text-green-600 text-sm">↑ 8.5% vs Previous Year</p>
            </div>
            <div className="bg-white p-4 rounded-lg shadow">
              <h3 className="text-gray-500 text-sm">Avg. Order Value</h3>
              <p className="text-2xl font-bold text-gray-800">{formatCurrency(405)}</p>
              <p className="text-green-600 text-sm">↑ 4.2% vs Previous Year</p>
            </div>
            <div className="bg-white p-4 rounded-lg shadow">
              <h3 className="text-gray-500 text-sm">Customer Retention</h3>
              <p className="text-2xl font-bold text-gray-800">76%</p>
              <p className="text-green-600 text-sm">↑ 3.1% vs Previous Year</p>
            </div>
          </div>

          {/* Quarterly Sales Trend */}
          <div className="bg-white p-4 rounded-lg shadow">
            <h3 className="text-lg font-semibold text-gray-800 mb-4">Quarterly Sales Trend</h3>
            <div className="h-64 flex items-end space-x-4 px-2">
              {quarterlyData.map((item) => {
                const height = (item.sales / 2000000) * 100;
                return (
                  <div key={item.quarter} className="flex-1 flex flex-col items-center">
                    <div className="w-full bg-blue-600 rounded-t" style={{height: `${height}%`}}></div>
                    <p className="text-sm font-medium mt-2">{item.quarter}</p>
                    <p className="text-xs text-gray-600">{formatCurrency(item.sales)}</p>
                  </div>
                );
              })}
            </div>
          </div>
          
          {/* Sales by Customer Journey Stage */}
          <div className="bg-white p-4 rounded-lg shadow">
            <h3 className="text-lg font-semibold text-gray-800 mb-4">Sales by Customer Journey Stage</h3>
            <div className="relative pt-1">
              <div className="flex mb-2 items-center justify-between">
                <div>
                  <span className="text-xs font-semibold inline-block py-1 px-2 uppercase rounded-full text-blue-600 bg-blue-200">
                    Awareness
                  </span>
                </div>
                <div className="text-right">
                  <span className="text-xs font-semibold inline-block text-blue-600">
                    15%
                  </span>
                </div>
              </div>
              <div className="overflow-hidden h-2 mb-4 text-xs flex rounded bg-blue-200">
                <div style={{ width: "15%" }} className="shadow-none flex flex-col text-center whitespace-nowrap text-white justify-center bg-blue-600"></div>
              </div>
              
              <div className="flex mb-2 items-center justify-between">
                <div>
                  <span className="text-xs font-semibold inline-block py-1 px-2 uppercase rounded-full text-purple-600 bg-purple-200">
                    Consideration
                  </span>
                </div>
                <div className="text-right">
                  <span className="text-xs font-semibold inline-block text-purple-600">
                    28%
                  </span>
                </div>
              </div>
              <div className="overflow-hidden h-2 mb-4 text-xs flex rounded bg-purple-200">
                <div style={{ width: "28%" }} className="shadow-none flex flex-col text-center whitespace-nowrap text-white justify-center bg-purple-600"></div>
              </div>
              
              <div className="flex mb-2 items-center justify-between">
                <div>
                  <span className="text-xs font-semibold inline-block py-1 px-2 uppercase rounded-full text-green-600 bg-green-200">
                    Purchase
                  </span>
                </div>
                <div className="text-right">
                  <span className="text-xs font-semibold inline-block text-green-600">
                    35%
                  </span>
                </div>
              </div>
              <div className="overflow-hidden h-2 mb-4 text-xs flex rounded bg-green-200">
                <div style={{ width: "35%" }} className="shadow-none flex flex-col text-center whitespace-nowrap text-white justify-center bg-green-600"></div>
              </div>
              
              <div className="flex mb-2 items-center justify-between">
                <div>
                  <span className="text-xs font-semibold inline-block py-1 px-2 uppercase rounded-full text-red-600 bg-red-200">
                    Retention
                  </span>
                </div>
                <div className="text-right">
                  <span className="text-xs font-semibold inline-block text-red-600">
                    22%
                  </span>
                </div>
              </div>
              <div className="overflow-hidden h-2 mb-4 text-xs flex rounded bg-red-200">
                <div style={{ width: "22%" }} className="shadow-none flex flex-col text-center whitespace-nowrap text-white justify-center bg-red-600"></div>
              </div>
            </div>
          </div>
        </div>
      )}

      {activeTab === 'segments' && (
        <div className="space-y-6">
          {/* Customer Segments */}
          <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
            <div className="bg-white p-4 rounded-lg shadow">
              <h3 className="text-lg font-semibold text-gray-800 mb-4">Customer Segments Distribution</h3>
              <div className="relative h-64">
                <div className="absolute inset-0 flex items-center justify-center">
                  <div className="w-48 h-48 rounded-full border-8 border-gray-200 relative">
                    <div className="absolute inset-0 border-t-8 border-l-8 border-blue-600 rounded-full" style={{transform: 'rotate(45deg)'}}></div>
                    <div className="absolute inset-0 border-t-8 border-l-8 border-green-600 rounded-full" style={{transform: 'rotate(165deg)'}}></div>
                    <div className="absolute inset-0 border-t-8 border-l-8 border-yellow-500 rounded-full" style={{transform: 'rotate(255deg)'}}></div>
                    <div className="absolute inset-0 border-t-8 border-l-8 border-red-500 rounded-full" style={{transform: 'rotate(345deg)'}}></div>
                  </div>
                </div>
                <div className="absolute top-2 left-2">
                  <div className="flex items-center">
                    <div className="w-3 h-3 bg-blue-600 rounded-full mr-2"></div>
                    <p className="text-sm">Champions (28%)</p>
                  </div>
                </div>
                <div className="absolute top-2 right-2">
                  <div className="flex items-center">
                    <div className="w-3 h-3 bg-green-600 rounded-full mr-2"></div>
                    <p className="text-sm">Potential Loyalists (42%)</p>
                  </div>
                </div>
                <div className="absolute bottom-2 left-2">
                  <div className="flex items-center">
                    <div className="w-3 h-3 bg-yellow-500 rounded-full mr-2"></div>
                    <p className="text-sm">At Risk (21%)</p>
                  </div>
                </div>
                <div className="absolute bottom-2 right-2">
                  <div className="flex items-center">
                    <div className="w-3 h-3 bg-red-500 rounded-full mr-2"></div>
                    <p className="text-sm">Needs Attention (9%)</p>
                  </div>
                </div>
              </div>
            </div>
            
            <div className="bg-white p-4 rounded-lg shadow">
              <h3 className="text-lg font-semibold text-gray-800 mb-4">Segment Performance</h3>
              <table className="min-w-full divide-y divide-gray-200">
                <thead className="bg-gray-50">
                  <tr>
                    <th className="px-3 py-2 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Segment</th>
                    <th className="px-3 py-2 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Avg. Spend</th>
                    <th className="px-3 py-2 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Retention</th>
                  </tr>
                </thead>
                <tbody className="bg-white divide-y divide-gray-200">
                  {segmentData.map((segment) => (
                    <tr key={segment.segment}>
                      <td className="px-3 py-2 whitespace-nowrap">
                        <div className="text-sm font-medium text-gray-900">{segment.segment}</div>
                      </td>
                      <td className="px-3 py-2 whitespace-nowrap">
                        <div className="text-sm text-gray-900">{formatCurrency(segment.avgSpend)}</div>
                      </td>
                      <td className="px-3 py-2 whitespace-nowrap">
                        <div className="text-sm text-gray-900">{segment.retention}%</div>
                      </td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </div>
          </div>
          
          {/* RFM Analysis */}
          <div className="bg-white p-4 rounded-lg shadow">
            <h3 className="text-lg font-semibold text-gray-800 mb-4">RFM Analysis</h3>
            <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
              <div className="p-3 border rounded-lg">
                <h4 className="text-base font-medium text-gray-800 mb-2">Recency</h4>
                <div className="space-y-2">
                  <div className="flex justify-between items-center">
                    <span className="text-xs">0-30 days</span>
                    <div className="w-2/3 bg-gray-200 rounded-full h-2.5">
                      <div className="bg-blue-600 h-2.5 rounded-full" style={{ width: '65%' }}></div>
                    </div>
                    <span className="text-xs">65%</span>
                  </div>
                  <div className="flex justify-between items-center">
                    <span className="text-xs">31-60 days</span>
                    <div className="w-2/3 bg-gray-200 rounded-full h-2.5">
                      <div className="bg-blue-600 h-2.5 rounded-full" style={{ width: '20%' }}></div>
                    </div>
                    <span className="text-xs">20%</span>
                  </div>
                  <div className="flex justify-between items-center">
                    <span className="text-xs">61-90 days</span>
                    <div className="w-2/3 bg-gray-200 rounded-full h-2.5">
                      <div className="bg-blue-600 h-2.5 rounded-full" style={{ width: '10%' }}></div>
                    </div>
                    <span className="text-xs">10%</span>
                  </div>
                  <div className="flex justify-between items-center">
                    <span className="text-xs">90+ days</span>
                    <div className="w-2/3 bg-gray-200 rounded-full h-2.5">
                      <div className="bg-blue-600 h-2.5 rounded-full" style={{ width: '5%' }}></div>
                    </div>
                    <span className="text-xs">5%</span>
                  </div>
                </div>
              </div>
              
              <div className="p-3 border rounded-lg">
                <h4 className="text-base font-medium text-gray-800 mb-2">Frequency</h4>
                <div className="space-y-2">
                  <div className="flex justify-between items-center">
                    <span className="text-xs">10+ purchases</span>
                    <div className="w-2/3 bg-gray-200 rounded-full h-2.5">
                      <div className="bg-green-600 h-2.5 rounded-full" style={{ width: '25%' }}></div>
                    </div>
                    <span className="text-xs">25%</span>
                  </div>
                  <div className="flex justify-between items-center">
                    <span className="text-xs">5-9 purchases</span>
                    <div className="w-2/3 bg-gray-200 rounded-full h-2.5">
                      <div className="bg-green-600 h-2.5 rounded-full" style={{ width: '35%' }}></div>
                    </div>
                    <span className="text-xs">35%</span>
                  </div>
                  <div className="flex justify-between items-center">
                    <span className="text-xs">2-4 purchases</span>
                    <div className="w-2/3 bg-gray-200 rounded-full h-2.5">
                      <div className="bg-green-600 h-2.5 rounded-full" style={{ width: '30%' }}></div>
                    </div>
                    <span className="text-xs">30%</span>
                  </div>
                  <div className="flex justify-between items-center">
                    <span className="text-xs">1 purchase</span>
                    <div className="w-2/3 bg-gray-200 rounded-full h-2.5">
                      <div className="bg-green-600 h-2.5 rounded-full" style={{ width: '10%' }}></div>
                    </div>
                    <span className="text-xs">10%</span>
                  </div>
                </div>
              </div>
              
              <div className="p-3 border rounded-lg">
                <h4 className="text-base font-medium text-gray-800 mb-2">Monetary</h4>
                <div className="space-y-2">
                  <div className="flex justify-between items-center">
                    <span className="text-xs">$1000+</span>
                    <div className="w-2/3 bg-gray-200 rounded-full h-2.5">
                      <div className="bg-purple-600 h-2.5 rounded-full" style={{ width: '20%' }}></div>
                    </div>
                    <span className="text-xs">20%</span>
                  </div>
                  <div className="flex justify-between items-center">
                    <span className="text-xs">$500-$999</span>
                    <div className="w-2/3 bg-gray-200 rounded-full h-2.5">
                      <div className="bg-purple-600 h-2.5 rounded-full" style={{ width: '30%' }}></div>
                    </div>
                    <span className="text-xs">30%</span>
                  </div>
                  <div className="flex justify-between items-center">
                    <span className="text-xs">$200-$499</span>
                    <div className="w-2/3 bg-gray-200 rounded-full h-2.5">
                      <div className="bg-purple-600 h-2.5 rounded-full" style={{ width: '35%' }}></div>
                    </div>
                    <span className="text-xs">35%</span>
                  </div>
                  <div className="flex justify-between items-center">
                    <span className="text-xs">$0-$199</span>
                    <div className="w-2/3 bg-gray-200 rounded-full h-2.5">
                      <div className="bg-purple-600 h-2.5 rounded-full" style={{ width: '15%' }}></div>
                    </div>
                    <span className="text-xs">15%</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      )}

      {activeTab === 'products' && (
        <div className="space-y-6">
          {/* Product Categories Performance */}
          <div className="bg-white p-4 rounded-lg shadow">
            <h3 className="text-lg font-semibold text-gray-800 mb-4">Product Categories Performance</h3>
            <table className="min-w-full divide-y divide-gray-200">
              <thead className="bg-gray-50">
                <tr>
                  <th className="px-3 py-2 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Category</th>
                  <th className="px-3 py-2 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Sales</th>
                  <th className="px-3 py-2 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Growth</th>
                  <th className="px-3 py-2 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Margin</th>
                  <th className="px-3 py-2 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Units Sold</th>
                </tr>
              </thead>
              <tbody className="bg-white divide-y divide-gray-200">
                {productData.map((product) => (
                  <tr key={product.category}>
                    <td className="px-3 py-2 whitespace-nowrap">
                      <div className="text-sm font-medium text-gray-900">{product.category}</div>
                    </td>
                    <td className="px-3 py-2 whitespace-nowrap">
                      <div className="text-sm text-gray-900">{formatCurrency(product.sales)}</div>
                    </td>
                    <td className="px-3 py-2 whitespace-nowrap">
                      <div className="text-sm text-green-600">+{product.growth}%</div>
                    </td>
                    <td className="px-3 py-2 whitespace-nowrap">
                      <div className="text-sm text-gray-900">{product.margin}%</div>
                    </td>
                    <td className="px-3 py-2 whitespace-nowrap">
                      <div className="text-sm text-gray-900">{product.units.toLocaleString()}</div>
                    </td>
                  </tr>
                ))}
              </tbody>
            </table>
          </div>
          
          {/* Sales by Product Category Visualization */}
          <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
            <div className="bg-white p-4 rounded-lg shadow">
              <h3 className="text-lg font-semibold text-gray-800 mb-4">Sales by Product Category</h3>
              <div className="h-64 flex items-end space-x-6 px-2">
                {productData.map((item) => {
                  const height = (item.sales / 1000000) * 100;
                  return (
                    <div key={item.category} className="flex-1 flex flex-col items-center">
                      <div className="w-full bg-indigo-600 rounded-t" style={{height: `${height}%`}}></div>
                      <p className="text-sm font-medium mt-2">{item.category}</p>
                      <p className="text-xs text-gray-600">{formatCurrency(item.sales)}</p>
                    </div>
                  );
                })}
              </div>
            </div>
            
            <div className="bg-white p-4 rounded-lg shadow">
              <h3 className="text-lg font-semibold text-gray-800 mb-4">Product Margin Comparison</h3>
              <div className="space-y-4">
                {productData.map((item) => (
                  <div key={item.category} className="space-y-1">
                    <div className="flex justify-between">
                      <span className="text-sm font-medium">{item.category}</span>
                      <span className="text-sm font-medium">{item.margin}%</span>
                    </div>
                    <div className="w-full bg-gray-200 rounded-full h-2.5">
                      <div 
                        className="bg-teal-600 h-2.5 rounded-full" 
                        style={{ width: `${item.margin * 2}%` }}
                      ></div>
                    </div>
                  </div>
                ))}
              </div>
            </div>
          </div>
        </div>
      )}
    </div>
  );
};

export default PowerBIDashboard;

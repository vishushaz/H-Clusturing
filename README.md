# H-Clusturing
Clustering the daily customers at supermarket 
Data = readtable('C:..\SuperMarket_Customers.csv');

td_AnnualIncome = (Data.AnnualIncome - mean(Data.AnnualIncome))/std(Data.AnnualIncome);
Data.AnnualIncome

Std_SpendingScore = (Data.SpendingScore - mean(Data.SpendingScore))/std(Data.SpendingScore);
Data.AnnualIncome

Data = Data(:,4:5);
Data = table2array(Data);


z = linkage(Data,'ward');


dendrogram(z);

I = inconsistent(z,6);
[a, b] = max(I(:,4));

c = cluster(z,'cutoff', z(b,3)-0.1,'Criterion','distance');

wcss = [];
for k = 1:10
    sumall = 0;
    [idx, C, sumall] = kmeans(Data, k);
    wcss(k) = sum(sumall);
end
plot(1:10, wcss);


[idx, C] = kmeans(Data,5);

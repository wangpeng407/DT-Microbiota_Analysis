# The digestive tract (DT) microbiota data analysis

## 1. Contribution of the ecological processes that determine community assembly

- Code is available at https://github.com/wangpeng407/assembly_proportion


## 2. Correlation heatmap 

- Code is available at https://github.com/wangpeng407/correlation_analysis


## 3. Sparcc correlation for co-occurence network

- Install [fastspar](https://github.com/scwatts/fastspar) first.

```
fastspar --iterations 50 --exclude_iterations 20 --otu_table filter.asv.xls  --correlation median_correlation.tsv --covariance median_covariance.tsv

mkdir bootstrap_counts
fastspar_bootstrap --otu_table filter.asv.xls  --number 1000 --prefix bootstrap_counts/fake_data
mkdir bootstrap_correlation

cd bootstrap_counts && ls *tsv | xargs -n 1   -I %  fastspar --otu_table % --correlation "../bootstrap_correlation/cor_%"  --covariance "../bootstrap_correlation/cov_%" --i 5 && cd ../

fastspar_pvalues --otu_table filter.asv.xls --correlation median_correlation.tsv --prefix bootstrap_correlation/cor_fake_data_ --permutations 1000 --outfile pvalues.tsv
```


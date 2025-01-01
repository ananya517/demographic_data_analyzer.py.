import pandas as pd

def race_count(df):
    return df['race'].value_counts()

def average_age_men(df):
    return df[df['sex'] == 'Male']['age'].mean()

def bachelors_percentage(df):
    return (df[df['education'] == 'Bachelors'].shape[0] / df.shape[0]) * 100

def advanced_education_percentage(df):
    advanced_education = df[df['education'].isin(['Bachelors', 'Masters', 'Doctorate'])]
    return (advanced_education[advanced_education['salary'] == '>50K'].shape[0] / advanced_education.shape[0]) * 100

def non_advanced_education_percentage(df):
    non_advanced_education = df[~df['education'].isin(['Bachelors', 'Masters', 'Doctorate'])]
    return (non_advanced_education[non_advanced_education['salary'] == '>50K'].shape[0] / non_advanced_education.shape[0]) * 100

def min_hours_per_week(df):
    return df['hours-per-week'].min()

def min_hours_more_than_50k_percentage(df, min_hours_per_week):
    min_hours_df = df[df['hours-per-week'] == min_hours_per_week]
    return (min_hours_df[min_hours_df['salary'] == '>50K'].shape[0] / min_hours_df.shape[0]) * 100

def highest_earning_country(df):
    country_salary_percentage = df.groupby('native-country').apply(lambda x: (x[x['salary'] == '>50K'].shape[0] / x.shape[0]) * 100)
    highest_earning_country = country_salary_percentage.idxmax()
    highest_earning_percentage = country_salary_percentage.max()
    return highest_earning_country, highest_earning_percentage

def most_popular_occupation_india(df):
    india_earning_more_50k = df[(df['native-country'] == 'India') & (df['salary'] == '>50K')]
    return india_earning_more_50k['occupation'].mode()[0]

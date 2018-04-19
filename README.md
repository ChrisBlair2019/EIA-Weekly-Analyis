# EIA-Weekly-Analysis
This is a program written in Python that automatically retrieves the EIA report summarizes it and converts it to an email format to email to the COINS group

# Control Flow
1. Run on an Amazon EC2 Instance running Ubuntu 16.04
2. Crontab that runs at 10:30 am EST in order to generate the report ("31 10 * * WED" Runs at 10:31am (account for timediff) every WED)
3. Runs shell script with error reporting 
4. Shell Script has 4 Steps
    1. First it runs Python Retrieve File "python get_EIA_PDFs.py"
        -This Retrieves the current report (Through URL)
        -Fetches last week's report (in Local Memory)
        -Fetches Report from the previous year (Through URL)
    2. Then on the report we run "pdf2txt.py highlights.pdf"
        -This converts each of the reports to <XX-XX-XXXX>.txt
    3. Run the python analysis file "EIA_Analysis.py"
        -This analyzes the txt file to get the classifer statistics that matter
        -Output an HTML file in order to make the email look nice
    4. Now run python email file "email.py" which emails the current list of emails
        -Stored locally, not publically in order to get the publication

# Steps to Parse the Input
1. Form the URL for the current report pdf 

    For the previous week 4/11/2018 URL looks like this
    https://www.eia.gov/petroleum/supply/weekly/archive/2018/2018_04_11/pdf/highlights.pdf

    For Week of 4/18/2018 URL looks like this (This is the current week URL everytime)
    http://ir.eia.gov/wpsr/wpsrsummary.pdf



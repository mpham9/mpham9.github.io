
<table>
  <tr>
    <td> </td>
    <td> R </td>
    <td> Python </td>
  </tr>
  
  <tr>
    <td> 
      Change directory 
    </td>
    <td>
      <pre lang="R">
      setwd("C:/temp")
      </pre>
    </td>
    <td>
      <pre lang="Python">
      import os
      os.chdir("C:\temp")
      </pre>
    </td>
  </tr>
  
  <tr>
    <td> Extract number using pattern </td>
    <td>
      <pre lang="R">
        library(NCmisc)
        library(stringr)
        res = list()
        j = 1
        df = readLines("filename.lp")
        for(i in 1:length(df)){
          if(str_detect(df[i],"(?<=\\+\\s)[0-9\\.]+(?=\\sConVio_N1_BuildLimit)")){
            print(df[i])
            print(str_extract_all(df[i],"(?<=\\+\\s)([0-9\\.]+)(?=\\sConVio_N1_BuildLimit)")[[1]])
            res1[[j]] = str_extract_all(df[i],"(?<=\\+\\s)([0-9\\.]+)(?=\\sConVio_N1_BuildLimit)")[[1]]
            j = j+1
          }
        }
      </pre>
      </td>
      <td><pre lang="Python">
            import re
            filename = "filename.lp"
            regex = '(?<=\\+\\s)[0-9\\.]+(?=\\sConVio_N1_BuildLimit)'
            match_list = []
            with open(filename, "r") as file:
                for line in file:
                    for match in re.finditer(regex, line):
                        match_text = match.group()
                        match_list.append(match_text)
                        print(line)           
            len([float(i) for i in match_list if float(i) != 0])
            sum([float(i) for i in match_list])
      </pre></td>
      </tr>
              
</table>

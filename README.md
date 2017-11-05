# Decompose

Decompose

把自然数Ｎ分解为若干个自然数之和。

【参考答案】

		 n     │ total  
     
		 5     │   7
     
		 6     │  11
     
		 7     │  15
     
		10     │  42
    
		100    │  190569291
    
【参考程序】

var n:byte; num:array[0..255] of byte;	total:word;

procedure output(dep:byte);

var j:byte;

begin

     for j:=1 to dep do write(num[j]:3);writeln;    inc(total);
     
end;

procedure find(n,dep:byte);  {N:待分解的数,DEP:深度}

  var i,j,rest:byte;
  
  begin
  
     for i:=1 to n do	  {每一位从N到1去试}
     
      if num[dep-1]<=i then   {保证选用的数大于前一位}
      
       begin
       
	 num[dep]:=i;
   
	 rest:=n - i;	      {剩余的数进行下一次递归调用}
   
	 if (rest>0) then begin   find(rest,dep+1);end
   
   
		     else if rest=0 then output(dep);{刚好相等则输出}
         
	 num[dep]:=0;
   
       end;
       
  end;
  

begin  {主程序}

   writeln('input n:');readln(n);
   
   fillchar(num,sizeof(num),0);
   
   total:=0; num[0]:=0;
   
   find(n,1);
   
   writeln('sum=',total);
   
end.


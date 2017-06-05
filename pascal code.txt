# Pascal-Program
var
   nmbrwhl, rand, num, temps : integer;
   nmbrspns, trspnss, count_num : longword;
   i, Secondcount, thridcount, secondgap, thirdgap : longword;
   even, odd, even_max, odd_max : longword;
   secondavg, thirdavg : double;
   rndmnmbr : array[0..200000000] of longword;

              {# Program starts from here #}

begin

writeln('Enter the number of Spins to start.');
readln(nmbrspns);

randomize;                             {# Initializing the instance of the Random Number Generator #}

nmbrwhl:=37;                         {# Defining the count of the total numbers on the wheel #}
Secondcount:=0;
thridcount:=0;
secondgap:=0;
thirdgap:=0;
trspnss:=0;

for i:=0 to nmbrspns do begin         {# Using the Loop through all the Spins of Random Numbers #}
    rand:=random(nmbrwhl);           {# Generating a random number #}
    rndmnmbr[i]:=rand;               {# Moving that random number that has been generated into an array #}
end;

for i:=0 to nmbrspns do begin         {# Using the Loop through all the Spins #}
    if(rndmnmbr[i]=rndmnmbr[i+1]) then begin   {# Verifying if two Consecutive Spins generate Equal Numbers #}
       Secondcount:=Secondcount+1;     {# If two Consecutive Numbers are found to be same, Increment the Counter #}
       secondgap:=secondgap+trspnss+1; {# Tracking of the Number of Spins between the two Consecutive Occurences of any number #}
       trspnss:=0;
    end else begin
       trspnss:=trspnss+1;           {# If two Consecutive Numbers yielded are NOT the Same, Increment the Gap Counter #}
    end;
end;

trspnss:=0; {# Re-initializing the Gap Counter to 0 (Zero) #}

for i:=0 to nmbrspns do begin          {# Begin to Loop through all the Spins #}
    if((rndmnmbr[i]=rndmnmbr[i+1]) and (rndmnmbr[i]=rndmnmbr[i+2])) then begin
                                        {# Verifying if three Consecutive Spins Produce Equal Numbers #}
       thridcount:=thridcount+1;    {# If three Consecutive Numbers are Same, then Increment the Counter #}
       thirdgap:=thirdgap+trspnss+1; {# Tracking the Number of Spins between the three Consecutive Occurences of any Number #}
       trspnss:=0;
    end else begin
       trspnss:=trspnss+1;            {# If three Consecutive Numbers are NOT the same ones, Increment the Gap Counter #}
    end;
end;

if(Secondcount>0) then begin
   secondavg:=(secondgap/Secondcount);
   writeln();
   writeln('The same numbers are repeated twice in a row for every  ',secondavg:1:2,'  numbers on an average.');
                                        {# Output 1: Average Frequency of occurences of a Number - TWICE in a row #}

end else begin
   writeln();
   writeln('No number repeats twice in a row');
end;
if(thridcount>0) then begin
   thirdavg:=(thirdgap/thridcount);
   writeln();
   writeln('The same numbers are repeated Thrice in a row for every  ',thirdavg:1:2,'  numbers on an average.');
                                        {# Output 2: Average Frequency of occurences of a Number - THRICE in a row #}

end else begin
   writeln();
   writeln('No number repeats thrice in a row');
end;

writeln();
writeln('choose a number between 1-36');
readln(num);                            {# Seeking the Input from the User for the Choice of the Number between 1-36 #}

trspnss:=0;

for i:=0 to nmbrspns do begin
    if(rndmnmbr[i]=num) then begin
        if(rndmnmbr[i]=rndmnmbr[i+1]) then begin
          count_num:=trspnss;
        end else begin
          trspnss:=trspnss+1;
        end;
    end else begin
        trspnss:=trspnss+1;
    end;
end;

if (count_num>0) then begin
 writeln();
 writeln(num,' is Repeated twice in a row after ',count_num,' numbers');
                                        {# Output 3: The Frequency of Occurences of a Specific Number - TWICE in a row #}
end else begin
 writeln();
 writeln(num,' is not repeated twice in a row');
end;

even_max:=0;                            {# The Max Count of two Consecutive Evens #}
even:=0;                          {# The Count of Longest Evens in a Row #}

odd_max:=0;                             {# The Max Count of two Consecutive Odds #}
odd:=0;                           {# The Count of Longest Evens in a Row #}

for i:=0 to num do begin
    if (rndmnmbr[i]<>0) then begin    {# Verifying if the Number is 0 (Zero) #}
         temps:=(rndmnmbr[i] mod 2);   {# If the Number is NOT zero, then Calculate the Remainder Using MOD Operator #}
         if (temps<>0) then begin        {# Verifying if the Number is Even (when mod=0) #}
            odd:=odd+1;     {# If the Number is Odd, then Increment the Count of Odds #}
            if (even>even_max) then begin
              even_max:=even;     {# The Longest Continuous occurences of EVENS is Calculated #}
            end;
            even:=0;
         end else begin
            even:=even+1;
            if (odd>odd_max) then begin
              odd_max:=odd;       {# The Longest Continuous occurence of ODDS is Calculated #}
            end;
            odd:=0;
         end;
    end;
end;

writeln();
writeln('The longest run of EVENS in a row = ',even_max);
                                        {# Output 4: The Longest Number of occurences of EVENS in a row #}
writeln();
writeln('The longest run of ODDS in a row = ',odd_max);
                                        {# Output 5: The Longest Number of occurences of ODDS in a row #}

writeln();
writeln('Press enter to exit');
readln();
End.
               {# Program ends here #}


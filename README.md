# hello-world
%Code for Student Assessment Analysis
classdef app1_backUP_another__ < matlab.apps.AppBase

    % Properties that correspond to app components
    properties (Access = public)
        UIFigure                        matlab.ui.Figure
        Lamp3_2                         matlab.ui.control.Lamp
        Lamp_6                          matlab.ui.control.Lamp
        Lamp_5                          matlab.ui.control.Lamp
        Lamp_4                          matlab.ui.control.Lamp
        Lamp11                          matlab.ui.control.Lamp
        Lamp10                          matlab.ui.control.Lamp
        Lamp8                           matlab.ui.control.Lamp
        Lamp7                           matlab.ui.control.Lamp
        Lamp6                           matlab.ui.control.Lamp
        Lamp5                           matlab.ui.control.Lamp
        Lamp4                           matlab.ui.control.Lamp
        Lamp3                           matlab.ui.control.Lamp
        Lamp2                           matlab.ui.control.Lamp
        Lamp_3                          matlab.ui.control.Lamp
        Lamp_2                          matlab.ui.control.Lamp
        Lamp                            matlab.ui.control.Lamp
        EditField_5                     matlab.ui.control.EditField
        FButton                         matlab.ui.control.Button
        histogramButton_9               matlab.ui.control.Button
        EditField_4                     matlab.ui.control.EditField
        EditField_3                     matlab.ui.control.EditField
        EditField6                      matlab.ui.control.EditField
        EditField5                      matlab.ui.control.EditField
        EditField4                      matlab.ui.control.EditField
        EditField3                      matlab.ui.control.EditField
        EditField2                      matlab.ui.control.EditField
        EditField_2                     matlab.ui.control.EditField
        histogramButton_8               matlab.ui.control.Button
        histogramButton_7               matlab.ui.control.Button
        histogramButton_6               matlab.ui.control.Button
        histogramButton_5               matlab.ui.control.Button
        histogramButton_4               matlab.ui.control.Button
        histogramButton_3               matlab.ui.control.Button
        histogramButton_2               matlab.ui.control.Button
        pieButton                       matlab.ui.control.Button
        FrequencyPolygonButton          matlab.ui.control.Button
        HistogramButton                 matlab.ui.control.Button
        AplusButton                     matlab.ui.control.Button
        StandarddeviationandAverageButton  matlab.ui.control.Button
        GradeButton                     matlab.ui.control.Button
        SortButton                      matlab.ui.control.Button
        Button                          matlab.ui.control.Button
        TotalNumberButton               matlab.ui.control.Button
        UITable2                        matlab.ui.control.Table
        ClickhereButton                 matlab.ui.control.Button
        InputValueinRowVectorFormEditField  matlab.ui.control.EditField
        InputValueinRowVectorFormEditFieldLabel  matlab.ui.control.Label
        EditField                       matlab.ui.control.EditField
        SemesterorCourseEditField       matlab.ui.control.EditField
        SemesterorCourseEditFieldLabel  matlab.ui.control.Label
        EnterFileNameEditField          matlab.ui.control.EditField
        EnterFileNameEditFieldLabel     matlab.ui.control.Label
        FileButton                      matlab.ui.control.Button
        UITable                         matlab.ui.control.Table
        UIAxes2                         matlab.ui.control.UIAxes
        UIAxes                          matlab.ui.control.UIAxes
    end

    
    properties (Access = private)
        filename;
        cors;% Description
        choice;
        allocated_percentage;
        credithours;
        ytable;
        Total_number;
        valuecheckgrade % goes to grade_num to find grade point
        transition; % Description
        prepercentage; % Description
        histogram_subject; % Description
    end
    
    methods (Access = private)
        
        function results = func(app)
             y=app.ytable;
            per=app.prepercentage;
            per=per./100;
             [a b]=size(y);
            for i=2:b
              c=y(:,i);
%               d=y(:,3);
            c=table2array(c);%d=table2array(d);e=c+d;
%                  e=array2table(e);
%                 y(:,i)=y(:,i)*per(i-1);
                 c=c.*per(i-1);
                c=array2table(c);
                y(:,i)=c;
        end
            z=zeros(a,1);
         for i=2:b
               e=y(:,i);
               e=table2array(e);
               z(:,1)=z(:,1)+e;
         end
         app.Total_number=z;
         results=z;
        end
        
        function results = grade_measure(app)

            y=app.ytable;
            cr=app.allocated_percentage;

            [a b]=size(y);


            for i=2:b
                for j=1:a
                    diate=y(j,i);
                    diate=table2array(diate);
                    app.valuecheckgrade=diate;
                  
                    diate=cr(i-1)*grade_num(app);
                   y(j,i)= array2table(diate);

                end

            end

            z=zeros(a,1);

            for i=2:b
                diate=y(:,i);
                diate=table2array(diate);
                z=z+diate;

            end
            c=z/sum(cr);
          
            c=array2table(c);
            results=c;

            
        end
        
        function results = grade_num(app)
            a=app.valuecheckgrade;
            if a>=80
                y=4;
            elseif a<80 & a>=75
                y=3.75;
            elseif a<75 & a>=70
                y=3.5;
            elseif a<70 & a>=65
                y=3.25;
            elseif a<65 & a>=60
                y=3;
            elseif a<60 & a>=55
                y=2.75;
            elseif a<55 & a>=50
                y=2.5;
            elseif a<50 & a>=45
                y=2.25;
            elseif a<45 & a>=40
                y=2;
            else
                y=0;
            end
            results=y;

        
        end
        function results = histogramplot(app)
             z=app.transition;
          [l b]=min(z);
        [h c]=max(z);
         n=round((h-l)^(1/2));

       hist= histogram(app.UIAxes,z,n);
       results=hist;
       set(hist,"Visible","Off");
       %hold on
            
        end
        
        function results = grade_course_imp(app)
                 z=func(app);
                 g=[0 0 0 0 0 0 0 0 0 0];
                 m=length(z);
            %g=table2array(g);
            for i=1:m
            if z(i)>=80
                g(1)=g(1)+1;
            elseif z(i)<80 & z(i)>=75
                 g(2)=g(2)+1;
            elseif z(i)<75 & z(i)>=70
                 g(3)=g(3)+1;
            elseif z(i)<70 & z(i)>=65 
                g(4)=g(4)+1;
            elseif z(i)<65 & z(i)>=60
                 g(5)=g(5)+1;
            elseif z(i)<60 & z(i)>=55
                 g(6)=g(6)+1;
            elseif z(i)<55 & z(i)>=50
                 g(7)=g(7)+1;
            elseif z(i)<50 & z(i)>=45
              g(8)=g(8)+1;
            elseif z(i)<45 & z(i)>=40
               g(9)=g(9)+1;
            else 
              g(10)=g(10)+1;
            end
            
            end
            results=g';
        end
        
        function results = histogram_grade_subject(app)
             z=app.histogram_subject;
          [l b]=min(z);
        [h c]=max(z);
         n=round((h-l)^(1/2));

       hist= histogram(app.UIAxes,z,n);

            
        end
    end

    % Callbacks that handle component events
    methods (Access = private)

        % Button pushed function: FileButton
        function FileButtonPushed(app, event)
            t= readtable(app.filename);
            app.UITable.Data=t;
            app.ytable=t;
            app.UITable.ColumnName=t.Properties.VariableNames;
        end

        % Value changed function: EnterFileNameEditField
        function EnterFileNameEditFieldValueChanged(app, event)
            value = app.EnterFileNameEditField.Value;
            app.filename=value;
        end

        % Callback function
        function PercentageEditFieldValueChanged(app, event)
            value = app.PercentageEditField.Value;
            app.cors=1;
            if app.cors==1
                app.PercentageEditField.Value="y";
            end
            
        end

        % Callback function
        function ExamTypeDropDownValueChanged(app, event)
            value = app.ExamTypeDropDown.Value;
            d=app.ExamTypeDropDown.Items;
            
            if strcmp("Semester",d)
                app.cors=1;
            else
                app.cors=0;
            end

        end

        % Value changed function: EditField
        function EditFieldValueChanged(app, event)
            value = app.EditField.Value;

           
            

        end

        % Value changed function: SemesterorCourseEditField
        function SemesterorCourseEditFieldValueChanged(app, event)
            value = app.SemesterorCourseEditField.Value;
            app.choice=value;

            if value =="Semester"
                app.Lamp_3.Color='r';
                app.Lamp2.Color ='r';
                app.Lamp3.Color='r'
                app.Lamp11.Color='r';
               
                app.Lamp_2.Color=[1 1 0];
                app.Lamp.Color=[1 1 0];
                app.Lamp_4.Color=[1 1 0];
               
                app.Lamp4.Color=[1 1 0];
                app.Lamp5.Color=[1 1 0];
                app.Lamp6.Color=[1 1 0];
                app.Lamp7.Color=[1 1 0];
                app.Lamp8.Color=[1 1 0];
                app.Lamp_5.Color=[1 1 0];
                app.Lamp_6.Color=[1 1 0];
                app.Lamp3_2.Color=[1 1 0];
                
                
                app.Lamp10.Color=[1 1 0];

            else

                 app.Lamp_3.Color= [1 1 0];
                app.Lamp2.Color = [1 1 0];
                app.Lamp3.Color= [1 1 0];
                app.Lamp11.Color= [1 1 0];
               
                app.Lamp_2.Color=[1 1 0];
                app.Lamp.Color=[1 1 0];
                app.Lamp_4.Color=[1 1 0];
               
                app.Lamp4.Color= 'r';
                app.Lamp5.Color= 'r';
                app.Lamp6.Color= 'r';
                app.Lamp7.Color= 'r'
                app.Lamp8.Color= 'r';
                app.Lamp_5.Color= 'r'
                app.Lamp_6.Color= 'r'
                app.Lamp3_2.Color= 'r'
                
                
                app.Lamp10.Color=[1 1 0];



                

                
            end

            

        end

        % Button pushed function: ClickhereButton
        function ClickhereButtonPushed(app, event)
            if strcmp(app.choice,"Semester")
                        app.EditField.Value="Credit Hours";
        
                         t=app.ytable;
        
                    variab=t.Properties.VariableNames;
        
                    a=length(variab);
                    variab=[variab "N/A" "N/A" "N/A" "N/A"];


        
                                if a>=1
                                    
                                    app.EditField_2.Value=char(variab(2));
                                   
                                    
                                    app.EditField3.Value= char(variab(3));
                                    
                               
                                    app.EditField_3.Value=char(variab(4));
                                   
                    
                                
                                    app.EditField4.Value = char(variab(5));
                                   
                    
                                
                                    app.EditField2.Value = char(variab(6));
                                    
                    
                                
                    
                                    app.EditField6.Value = char(variab(7));
                                   
                    
                                
                    
                                    app.EditField5.Value = char(variab(8));
                                    
                              
                                    app.EditField_4.Value = char(variab(9));
                                end

            else
                 app.EditField.Value="Percentage allocation";
            end
        end

        % Value changed function: InputValueinRowVectorFormEditField
        function InputValueinRowVectorFormEditFieldValueChanged(app, event)
            value = app.InputValueinRowVectorFormEditField.Value;
            app.allocated_percentage=str2num(value);
            app.prepercentage=app.allocated_percentage;
            func(app);
        end

        % Button pushed function: TotalNumberButton
        function TotalNumberButtonPushed(app, event)
            y=app.ytable; %y=table2cell(y);
            z=func(app);
            Total_Marks=z;
           Total_Marks= array2table(Total_Marks);
         

           app.UITable2.Data=Total_Marks;
           app.UITable2.ColumnName=Total_Marks.Properties.VariableNames;
           
           %Excel file
           t= app.UITable2.Data;
           writetable(t,"Total Marks.xlsx","Sheet",1);


        end

        % Button pushed function: SortButton
        function SortButtonPushed(app, event)
           
                           
            if strcmp("Course",app.choice)
            
                           y=app.ytable; %y=table2cell(y);
                
                           z=func(app);
                           A=app.ytable;
                           [M I]=sort(z,"descend");
                           s=[];
                           n=length(z);
                           Total_Marks=zeros(n,1);
                    
                           for i=1:n
                                   Total_Marks=z(I(i));
                                   Total_Marks=array2table(Total_Marks);
                                   s=[s;A(I(i),:) Total_Marks];
                            end
                
                            app.UITable2.Data=s;
                            app.UITable2.ColumnName=s.Properties.VariableNames;
                             
                            t=app.UITable2.Data;
                            writetable(t,"Sorted.xlsx","Sheet",1);

            else

                 y=app.ytable;
                 z=grade_measure(app);
                 z=table2array(z);
                 A=app.ytable;
                 [M I]=sort(z,"descend");
                 s=[];
                 n=length(z);
                 Grade_points=zeros(n,1);

                 for i=1:n
                     Grade_points=z(I(i));
                     Grade_points=array2table(Grade_points);
                     s=[s;A(I(i),:) Grade_points];
                 end

                 app.UITable2.Data=s;
                 app.UITable2.ColumnName=s.Properties.VariableNames;
                  t=app.UITable2.Data;
                  writetable(t,"Sorted Grade Points.xlsx","Sheet",1);




            end



                            

        end

        % Cell edit callback: UITable
        function UITableCellEdit(app, event)
            indices = event.Indices;
            newData = event.NewData;
            
        end

        % Button pushed function: GradeButton
        function GradeButtonPushed(app, event)
             if strcmp(app.choice,"Course")
            y=app.ytable; %y=table2cell(y);


Number=grade_course_imp(app);

Grade_type=["A+" ; "A";  "A-" ; "B+";"B";"B-";"C+";"C";"D";"F"];

t1=table(Grade_type,Number);

app.UITable2.Data=t1;
app.UITable2.ColumnName=t1.Properties.VariableNames;

            
             else
                GradePoint= grade_measure(app);

                app.UITable2.Data=[app.ytable GradePoint];

                t=[app.ytable GradePoint];
                [rows cols]=size(t);
                t.Properties.VariableNames(cols)="Grade Points";

                app.UITable2.ColumnName=t.Properties.VariableNames;

                writetable(t,"GradePoints.xlsx","Sheet",1);



             end 

        


        
        end

        % Button pushed function: StandarddeviationandAverageButton
        function StandarddeviationandAverageButtonPushed(app, event)
             y=app.ytable; %y=table2cell(y);
            % z=func(app);
             [a b]=size(y);
             z=zeros(a,1);
           
             for i=2:b
                 c=y(:,i);
                 c=table2array(c);
                 z=z+c;
             end


             
         avg=z./(b-1);
         sum=0;

         for i=2:b
             c=y(:,i);
             c=table2array(c);
             sum = (c-avg).^2+sum;
         end
         sum=sum./(b-1);
 
         sum=sum.^(1/2);
         standard_deviation=sum;
         %%%

        standard_deviation =array2table(standard_deviation);
        avg=array2table(avg);

        y=app.ytable;
        %standard_deviation =sum;
        %standard_deviation=array2table(standard_deviation);
        
        t1=[y avg standard_deviation];

      %  t1.Properties.VariableNames=y.Properties.VariableNames,'average','deviate';

        app.UITable2.Data = t1;
        app.UITable2.ColumnName= t1.Properties.VariableNames;
       


         t=app.UITable2.Data;
         writetable(t,"Standard_deviation.xlsx","Sheet",1);


         




        end

        % Button pushed function: AplusButton
        function AplusButtonPushed(app, event)
            % 1

        per=app.allocated_percentage;
            len=length(per);
     per=  [per 0 0 0 0 0 0];
    %yper=per;
   Aplus=0;
   
       for i=per(1)-5:1:per(1)+5
         for j=per(2)-5:1:per(2)+5

           for k=per(3)-5:1:per(3)+5
               if len<3
                   kl=0;
               else
                   kl=k;
               end
                
             for l=per(4)-5:1:per(4)+5
                 if len<4
                     ll=0;
                 else
                     ll=l;
                 end
                 
                  for m=per(5)-5:1:per(5)+5
                      if len<5
                          ml=0;
                      else
                          ml=m;
                      end
                     
                      
                          
                if (i+j+kl+ll+ml)~=100 
                    continue;
                else
                    app.prepercentage=[i j kl ll ml];
                    h=grade_course_imp(app);
                    if h(1)>= Aplus
                        Aplus=h(1);
                       c= app.prepercentage;
                    end
               

                end
             end
           end
         end
           end
         end
       
           % 3

       c=array2table(c);
       app.UITable2.Data=c;


       
        end

        % Button pushed function: HistogramButton
        function HistogramButtonPushed(app, event)
           hold(app.UIAxes,"Off");
            func(app);
            z=app.Total_number;
          [l b]=min(z);
        [h c]=max(z);
         n=round((h-l)^(1/2));

       hist= histogram(app.UIAxes,z,n);
       histogram(app.UIAxes,z,n)
      % set(hist,"Visible","Off");
       
        end

        % Button pushed function: FrequencyPolygonButton
        function FrequencyPolygonButtonPushed(app, event)
            y=app.ytable;;
%             y=table2array(y);
%             y=str2double(y);
            
            [q w]=size(y);
            
            for i=2:w
                  
            %m=hist_ogram(y(:,i));
                    c=y(:,i);
                    c=table2array(c);
                    app.transition=c;
                    m=histogramplot(app)
                    mat=[];
                    d=m.BinEdges;
                    n=length(d);
                    for k=1:n-1
                        a=[(d(k)+d(k+1))/2];
                        mat=[mat a];
                    end
                    e=m.Values;

  
            var = y.Properties.VariableNames;
            ch=char(var(i));
            plot(app.UIAxes,mat,e,"DisplayName",ch);
            
            %legend(app.UIAxes);

            hold(app.UIAxes,"on")
            end

            hold (app.UIAxes,"off");

            legend(app.UIAxes);

            % legend()
            %legend(app.UIAxes,'1','2','3','4','5','6');
        end

        % Callback function
        function pieButtonPushed(app, event)
            Number=grade_course_imp(app);
            pie(app.UIAxes,Number,{'Aplus','A','Aminus','Bplus','B','Bminus','Cplus','C','D','F'});

        end

        % Button pushed function: pieButton
        function pieButtonPushed2(app, event)
             Number=grade_course_imp(app);
            pie(app.UIAxes2,Number,{'Aplus','A','Aminus','Bplus','B','Bminus','Cplus','C','D','F'});
        end

        % Value changed function: EditField_2
        function EditField_2ValueChanged(app, event)
            value = app.EditField_2.Value;
            

        end

        % Value changed function: EditField3
        function EditField3ValueChanged(app, event)
            value = app.EditField3.Value;
            
        end

        % Value changed function: EditField_3
        function EditField_3ValueChanged(app, event)
            value = app.EditField_3.Value;
            
        end

        % Value changed function: EditField4
        function EditField4ValueChanged(app, event)
            value = app.EditField4.Value;
            
        end

        % Value changed function: EditField2
        function EditField2ValueChanged(app, event)
            value = app.EditField2.Value;
            
        end

        % Value changed function: EditField6
        function EditField6ValueChanged(app, event)
            value = app.EditField6.Value;
            
        end

        % Value changed function: EditField5
        function EditField5ValueChanged(app, event)
            value = app.EditField5.Value;
            
        end

        % Value changed function: EditField_4
        function EditField_4ValueChanged(app, event)
            value = app.EditField_4.Value;
            
        end

        % Callback function
        function histogramButtonPushed(app, event)
            c=app.ytable;
            d=c(:,2);
            d=table2array(d);
            app.histogram_subject=d;
            
            histogram_grade_subject(app);


        end

        % Cell edit callback: UITable2
        function UITable2CellEdit(app, event)
            indices = event.Indices;
            newData = event.NewData;
            
        end

        % Button pushed function: histogramButton_2
        function histogramButton_2Pushed(app, event)
             c=app.ytable;
            d=c(:,3);
            d=table2array(d);
            app.histogram_subject=d;
            
            histogram_grade_subject(app);
        end

        % Button pushed function: histogramButton_3
        function histogramButton_3Pushed(app, event)
             c=app.ytable;
            d=c(:,4);
            d=table2array(d);
            app.histogram_subject=d;
            
            histogram_grade_subject(app);
        end

        % Button pushed function: histogramButton_4
        function histogramButton_4Pushed(app, event)
             c=app.ytable;
            d=c(:,5);
            d=table2array(d);
            app.histogram_subject=d;
            
            histogram_grade_subject(app);
        end

        % Button pushed function: histogramButton_5
        function histogramButton_5Pushed(app, event)
             c=app.ytable;
            d=c(:,6);
            d=table2array(d);
            app.histogram_subject=d;
            
            histogram_grade_subject(app);
        end

        % Button pushed function: histogramButton_6
        function histogramButton_6Pushed(app, event)
             c=app.ytable;
            d=c(:,7);
            d=table2array(d);
            app.histogram_subject=d;
            
            histogram_grade_subject(app);
        end

        % Button pushed function: histogramButton_7
        function histogramButton_7Pushed(app, event)
             c=app.ytable;
            d=c(:,8);
            d=table2array(d);
            app.histogram_subject=d;
            
            histogram_grade_subject(app);
        end

        % Button pushed function: histogramButton_8
        function histogramButton_8Pushed(app, event)
             c=app.ytable;
            d=c(:,9);
            d=table2array(d);
            app.histogram_subject=d;
            
            histogram_grade_subject(app);
        end

        % Button pushed function: histogramButton_9
        function histogramButton_9Pushed(app, event)
             c=app.ytable;
            d=c(:,2);
            d=table2array(d);
            app.histogram_subject=d;
            
            histogram_grade_subject(app);
        end

        % Button pushed function: FButton
        function FButtonPushed(app, event)
             % 1

        per=app.allocated_percentage;
            len=length(per);
     per=  [per 0 0 0 0 0 0];
     [rows cols]=size(app.ytable);
    %yper=per;
  % Aplus=0;
   fgrade=rows;
   
       for i=per(1)-5:1:per(1)+5
         for j=per(2)-5:1:per(2)+5

           for k=per(3)-5:1:per(3)+5
               if len<3
                   kl=0;
               else
                   kl=k;
               end
                
             for l=per(4)-5:1:per(4)+5
                 if len<4
                     ll=0;
                 else
                     ll=l;
                 end
                 
                  for m=per(5)-5:1:per(5)+5
                      if len<5
                          ml=0;
                      else
                          ml=m;
                      end
                     
                      
                          
                if (i+j+kl+ll+ml)~=100 
                    continue;
                else
                    app.prepercentage=[i j kl ll ml];
                    h=grade_course_imp(app);
                    if h(10)<= fgrade
                        fgrade=h(10);
                       c= app.prepercentage;
                    end
               
%%
                end
             end
           end
         end
           end
         end
       
           
       c=array2table(c);
       app.UITable2.Data=c;

        end

        % Button down function: UIAxes
        function UIAxesButtonDown(app, event)
            
        end

        % Button down function: UIAxes2
        function UIAxes2ButtonDown(app, event)
            
        end
    end

    % Component initialization
    methods (Access = private)

        % Create UIFigure and components
        function createComponents(app)

            % Create UIFigure and hide until all components are created
            app.UIFigure = uifigure('Visible', 'off');
            app.UIFigure.Position = [100 100 1797 860];
            app.UIFigure.Name = 'MATLAB App';

            % Create UIAxes
            app.UIAxes = uiaxes(app.UIFigure);
            title(app.UIAxes, 'Title')
            xlabel(app.UIAxes, 'X')
            ylabel(app.UIAxes, 'Y')
            zlabel(app.UIAxes, 'Z')
            app.UIAxes.ButtonDownFcn = createCallbackFcn(app, @UIAxesButtonDown, true);
            app.UIAxes.Position = [618 257 690 409];

            % Create UIAxes2
            app.UIAxes2 = uiaxes(app.UIFigure);
            title(app.UIAxes2, 'Pie Chart')
            xlabel(app.UIAxes2, 'X')
            ylabel(app.UIAxes2, 'Y')
            zlabel(app.UIAxes2, 'Z')
            app.UIAxes2.ButtonDownFcn = createCallbackFcn(app, @UIAxes2ButtonDown, true);
            app.UIAxes2.Position = [952 19 356 239];

            % Create UITable
            app.UITable = uitable(app.UIFigure);
            app.UITable.ColumnName = {'Column 1'; 'Column 2'; 'Column 3'; 'Column 4'};
            app.UITable.RowName = {};
            app.UITable.CellEditCallback = createCallbackFcn(app, @UITableCellEdit, true);
            app.UITable.Position = [37 445 169 132];

            % Create FileButton
            app.FileButton = uibutton(app.UIFigure, 'push');
            app.FileButton.ButtonPushedFcn = createCallbackFcn(app, @FileButtonPushed, true);
            app.FileButton.Position = [266 797 100 22];
            app.FileButton.Text = 'File';

            % Create EnterFileNameEditFieldLabel
            app.EnterFileNameEditFieldLabel = uilabel(app.UIFigure);
            app.EnterFileNameEditFieldLabel.HorizontalAlignment = 'right';
            app.EnterFileNameEditFieldLabel.Position = [18 797 92 22];
            app.EnterFileNameEditFieldLabel.Text = 'Enter File Name';

            % Create EnterFileNameEditField
            app.EnterFileNameEditField = uieditfield(app.UIFigure, 'text');
            app.EnterFileNameEditField.ValueChangedFcn = createCallbackFcn(app, @EnterFileNameEditFieldValueChanged, true);
            app.EnterFileNameEditField.Position = [125 797 100 22];

            % Create SemesterorCourseEditFieldLabel
            app.SemesterorCourseEditFieldLabel = uilabel(app.UIFigure);
            app.SemesterorCourseEditFieldLabel.HorizontalAlignment = 'right';
            app.SemesterorCourseEditFieldLabel.Position = [11 758 113 22];
            app.SemesterorCourseEditFieldLabel.Text = 'Semester or Course';

            % Create SemesterorCourseEditField
            app.SemesterorCourseEditField = uieditfield(app.UIFigure, 'text');
            app.SemesterorCourseEditField.ValueChangedFcn = createCallbackFcn(app, @SemesterorCourseEditFieldValueChanged, true);
            app.SemesterorCourseEditField.Position = [139 758 100 22];

            % Create EditField
            app.EditField = uieditfield(app.UIFigure, 'text');
            app.EditField.ValueChangedFcn = createCallbackFcn(app, @EditFieldValueChanged, true);
            app.EditField.Position = [21 655 189 22];

            % Create InputValueinRowVectorFormEditFieldLabel
            app.InputValueinRowVectorFormEditFieldLabel = uilabel(app.UIFigure);
            app.InputValueinRowVectorFormEditFieldLabel.HorizontalAlignment = 'right';
            app.InputValueinRowVectorFormEditFieldLabel.Position = [10 591 174 22];
            app.InputValueinRowVectorFormEditFieldLabel.Text = 'Input Value in Row Vector Form';

            % Create InputValueinRowVectorFormEditField
            app.InputValueinRowVectorFormEditField = uieditfield(app.UIFigure, 'text');
            app.InputValueinRowVectorFormEditField.ValueChangedFcn = createCallbackFcn(app, @InputValueinRowVectorFormEditFieldValueChanged, true);
            app.InputValueinRowVectorFormEditField.Position = [199 591 127 22];

            % Create ClickhereButton
            app.ClickhereButton = uibutton(app.UIFigure, 'push');
            app.ClickhereButton.ButtonPushedFcn = createCallbackFcn(app, @ClickhereButtonPushed, true);
            app.ClickhereButton.Position = [18 709 100 22];
            app.ClickhereButton.Text = 'Click here';

            % Create UITable2
            app.UITable2 = uitable(app.UIFigure);
            app.UITable2.ColumnName = {'Column 1'; 'Column 2'; 'Column 3'; 'Column 4'};
            app.UITable2.RowName = {};
            app.UITable2.CellEditCallback = createCallbackFcn(app, @UITable2CellEdit, true);
            app.UITable2.Position = [334 525 245 185];

            % Create TotalNumberButton
            app.TotalNumberButton = uibutton(app.UIFigure, 'push');
            app.TotalNumberButton.ButtonPushedFcn = createCallbackFcn(app, @TotalNumberButtonPushed, true);
            app.TotalNumberButton.Position = [18 381 100 22];
            app.TotalNumberButton.Text = 'Total Number';

            % Create Button
            app.Button = uibutton(app.UIFigure, 'push');
            app.Button.Position = [-85 921 2 2];

            % Create SortButton
            app.SortButton = uibutton(app.UIFigure, 'push');
            app.SortButton.ButtonPushedFcn = createCallbackFcn(app, @SortButtonPushed, true);
            app.SortButton.Position = [139 381 100 22];
            app.SortButton.Text = 'Sort';

            % Create GradeButton
            app.GradeButton = uibutton(app.UIFigure, 'push');
            app.GradeButton.ButtonPushedFcn = createCallbackFcn(app, @GradeButtonPushed, true);
            app.GradeButton.Position = [266 381 100 22];
            app.GradeButton.Text = 'Grade';

            % Create StandarddeviationandAverageButton
            app.StandarddeviationandAverageButton = uibutton(app.UIFigure, 'push');
            app.StandarddeviationandAverageButton.ButtonPushedFcn = createCallbackFcn(app, @StandarddeviationandAverageButtonPushed, true);
            app.StandarddeviationandAverageButton.Position = [388 381 205 22];
            app.StandarddeviationandAverageButton.Text = 'Standard deviation and Average';

            % Create AplusButton
            app.AplusButton = uibutton(app.UIFigure, 'push');
            app.AplusButton.ButtonPushedFcn = createCallbackFcn(app, @AplusButtonPushed, true);
            app.AplusButton.Position = [362 11 88 22];
            app.AplusButton.Text = 'Aplus';

            % Create HistogramButton
            app.HistogramButton = uibutton(app.UIFigure, 'push');
            app.HistogramButton.ButtonPushedFcn = createCallbackFcn(app, @HistogramButtonPushed, true);
            app.HistogramButton.Position = [139 328 100 22];
            app.HistogramButton.Text = 'Histogram';

            % Create FrequencyPolygonButton
            app.FrequencyPolygonButton = uibutton(app.UIFigure, 'push');
            app.FrequencyPolygonButton.ButtonPushedFcn = createCallbackFcn(app, @FrequencyPolygonButtonPushed, true);
            app.FrequencyPolygonButton.Position = [500 11 119 22];
            app.FrequencyPolygonButton.Text = 'Frequency Polygon';

            % Create pieButton
            app.pieButton = uibutton(app.UIFigure, 'push');
            app.pieButton.ButtonPushedFcn = createCallbackFcn(app, @pieButtonPushed2, true);
            app.pieButton.Position = [18 328 100 22];
            app.pieButton.Text = 'pie';

            % Create histogramButton_2
            app.histogramButton_2 = uibutton(app.UIFigure, 'push');
            app.histogramButton_2.ButtonPushedFcn = createCallbackFcn(app, @histogramButton_2Pushed, true);
            app.histogramButton_2.Position = [164 214 100 22];
            app.histogramButton_2.Text = 'histogram';

            % Create histogramButton_3
            app.histogramButton_3 = uibutton(app.UIFigure, 'push');
            app.histogramButton_3.ButtonPushedFcn = createCallbackFcn(app, @histogramButton_3Pushed, true);
            app.histogramButton_3.Position = [305 214 100 22];
            app.histogramButton_3.Text = 'histogram';

            % Create histogramButton_4
            app.histogramButton_4 = uibutton(app.UIFigure, 'push');
            app.histogramButton_4.ButtonPushedFcn = createCallbackFcn(app, @histogramButton_4Pushed, true);
            app.histogramButton_4.Position = [450 214 100 22];
            app.histogramButton_4.Text = 'histogram';

            % Create histogramButton_5
            app.histogramButton_5 = uibutton(app.UIFigure, 'push');
            app.histogramButton_5.ButtonPushedFcn = createCallbackFcn(app, @histogramButton_5Pushed, true);
            app.histogramButton_5.Position = [346 109 100 22];
            app.histogramButton_5.Text = 'histogram';

            % Create histogramButton_6
            app.histogramButton_6 = uibutton(app.UIFigure, 'push');
            app.histogramButton_6.ButtonPushedFcn = createCallbackFcn(app, @histogramButton_6Pushed, true);
            app.histogramButton_6.Position = [500 109 100 22];
            app.histogramButton_6.Text = 'histogram';

            % Create histogramButton_7
            app.histogramButton_7 = uibutton(app.UIFigure, 'push');
            app.histogramButton_7.ButtonPushedFcn = createCallbackFcn(app, @histogramButton_7Pushed, true);
            app.histogramButton_7.Position = [24 109 100 22];
            app.histogramButton_7.Text = 'histogram';

            % Create histogramButton_8
            app.histogramButton_8 = uibutton(app.UIFigure, 'push');
            app.histogramButton_8.ButtonPushedFcn = createCallbackFcn(app, @histogramButton_8Pushed, true);
            app.histogramButton_8.Position = [180 109 100 22];
            app.histogramButton_8.Text = 'histogram';

            % Create EditField_2
            app.EditField_2 = uieditfield(app.UIFigure, 'text');
            app.EditField_2.ValueChangedFcn = createCallbackFcn(app, @EditField_2ValueChanged, true);
            app.EditField_2.Position = [29 256 93 22];

            % Create EditField2
            app.EditField2 = uieditfield(app.UIFigure, 'text');
            app.EditField2.ValueChangedFcn = createCallbackFcn(app, @EditField2ValueChanged, true);
            app.EditField2.Position = [346 151 100 22];

            % Create EditField3
            app.EditField3 = uieditfield(app.UIFigure, 'text');
            app.EditField3.ValueChangedFcn = createCallbackFcn(app, @EditField3ValueChanged, true);
            app.EditField3.Position = [164 256 100 22];

            % Create EditField4
            app.EditField4 = uieditfield(app.UIFigure, 'text');
            app.EditField4.ValueChangedFcn = createCallbackFcn(app, @EditField4ValueChanged, true);
            app.EditField4.Position = [449 256 100 22];

            % Create EditField5
            app.EditField5 = uieditfield(app.UIFigure, 'text');
            app.EditField5.ValueChangedFcn = createCallbackFcn(app, @EditField5ValueChanged, true);
            app.EditField5.Position = [26 151 100 22];

            % Create EditField6
            app.EditField6 = uieditfield(app.UIFigure, 'text');
            app.EditField6.ValueChangedFcn = createCallbackFcn(app, @EditField6ValueChanged, true);
            app.EditField6.Position = [500 151 100 22];

            % Create EditField_3
            app.EditField_3 = uieditfield(app.UIFigure, 'text');
            app.EditField_3.ValueChangedFcn = createCallbackFcn(app, @EditField_3ValueChanged, true);
            app.EditField_3.Position = [305 256 100 22];

            % Create EditField_4
            app.EditField_4 = uieditfield(app.UIFigure, 'text');
            app.EditField_4.ValueChangedFcn = createCallbackFcn(app, @EditField_4ValueChanged, true);
            app.EditField_4.Position = [180 151 100 22];

            % Create histogramButton_9
            app.histogramButton_9 = uibutton(app.UIFigure, 'push');
            app.histogramButton_9.ButtonPushedFcn = createCallbackFcn(app, @histogramButton_9Pushed, true);
            app.histogramButton_9.Position = [26 206 100 22];
            app.histogramButton_9.Text = 'histogram';

            % Create FButton
            app.FButton = uibutton(app.UIFigure, 'push');
            app.FButton.ButtonPushedFcn = createCallbackFcn(app, @FButtonPushed, true);
            app.FButton.Position = [75 11 100 22];
            app.FButton.Text = 'F';

            % Create EditField_5
            app.EditField_5 = uieditfield(app.UIFigure, 'text');
            app.EditField_5.Position = [132 52 273 22];
            app.EditField_5.Value = 'Grade Improvement Percentage';

            % Create Lamp
            app.Lamp = uilamp(app.UIFigure);
            app.Lamp.Position = [306 410 20 20];
            app.Lamp.Color = [1 0.4118 0.1608];

            % Create Lamp_2
            app.Lamp_2 = uilamp(app.UIFigure);
            app.Lamp_2.Position = [190 409 20 20];
            app.Lamp_2.Color = [1 0.4118 0.1608];

            % Create Lamp_3
            app.Lamp_3 = uilamp(app.UIFigure);
            app.Lamp_3.Position = [58 410 20 20];
            app.Lamp_3.Color = [1 0.4118 0.1608];

            % Create Lamp2
            app.Lamp2 = uilamp(app.UIFigure);
            app.Lamp2.Position = [63 359 20 20];
            app.Lamp2.Color = [1 0.4118 0.1608];

            % Create Lamp3
            app.Lamp3 = uilamp(app.UIFigure);
            app.Lamp3.Position = [182 359 20 20];
            app.Lamp3.Color = [1 0.4118 0.1608];

            % Create Lamp4
            app.Lamp4 = uilamp(app.UIFigure);
            app.Lamp4.Position = [82 290 20 20];
            app.Lamp4.Color = [1 0.4118 0.1608];

            % Create Lamp5
            app.Lamp5 = uilamp(app.UIFigure);
            app.Lamp5.Position = [207 290 20 20];
            app.Lamp5.Color = [1 0.4118 0.1608];

            % Create Lamp6
            app.Lamp6 = uilamp(app.UIFigure);
            app.Lamp6.Position = [346 290 20 20];
            app.Lamp6.Color = [1 0.4118 0.1608];

            % Create Lamp7
            app.Lamp7 = uilamp(app.UIFigure);
            app.Lamp7.Position = [481 290 20 20];
            app.Lamp7.Color = [1 0.4118 0.1608];

            % Create Lamp8
            app.Lamp8 = uilamp(app.UIFigure);
            app.Lamp8.Position = [64 185 20 20];
            app.Lamp8.Color = [1 0.4118 0.1608];

            % Create Lamp10
            app.Lamp10 = uilamp(app.UIFigure);
            app.Lamp10.Position = [540 53 20 20];
            app.Lamp10.Color = [1 0.4118 0.1608];

            % Create Lamp11
            app.Lamp11 = uilamp(app.UIFigure);
            app.Lamp11.Position = [231 82 20 20];
            app.Lamp11.Color = [1 0.4118 0.1608];

            % Create Lamp_4
            app.Lamp_4 = uilamp(app.UIFigure);
            app.Lamp_4.Position = [490 409 20 20];
            app.Lamp_4.Color = [1 0.4118 0.1608];

            % Create Lamp_5
            app.Lamp_5 = uilamp(app.UIFigure);
            app.Lamp_5.Position = [229 185 20 20];
            app.Lamp_5.Color = [1 0.4118 0.1608];

            % Create Lamp_6
            app.Lamp_6 = uilamp(app.UIFigure);
            app.Lamp_6.Position = [385 185 20 20];
            app.Lamp_6.Color = [1 0.4118 0.1608];

            % Create Lamp3_2
            app.Lamp3_2 = uilamp(app.UIFigure);
            app.Lamp3_2.Position = [540 185 20 20];
            app.Lamp3_2.Color = [1 0.4118 0.1608];

            % Show the figure after all components are created
            app.UIFigure.Visible = 'on';
        end
    end

    % App creation and deletion
    methods (Access = public)

        % Construct app
        function app = app1_backUP_another__

            % Create UIFigure and components
            createComponents(app)

            % Register the app with App Designer
            registerApp(app, app.UIFigure)

            if nargout == 0
                clear app
            end
        end

        % Code that executes before app deletion
        function delete(app)

            % Delete UIFigure when app is deleted
            delete(app.UIFigure)
        end
    end
en


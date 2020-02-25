# all-about-javascript

1. **Hoisting, var, let, const, functions** - როდესაც ჯს ენჯაინი მიიღებს კოდს გასაშვებად, პირველ რიგში მემორიში გამოყოფს ადგილს, რომ შეინახოს ფუნცქციები და ცვლადები. ფუნქციები, როგორც წესი ინახები რეფერენსებად და დარეგისტრირებული ფუნქციის value ყოველთვის არის <function>-ი. რაც შეეხება ცვლადებს,es6-ს ახალი ტიპები let და const-ის ცვლადები ინახება, როგორც <uninitialized> , ხოლო var-ი ინახება როგორც undefined.
  
  
2. **context(this)** - ყველა ფუნქციას გააჩნია კონტექსტი, რომელიც მიუთითებს იმ ობიექტს რომელსაც ეკუთხვნის ეს ფუნქცია. როგორც წესი ჩვეულებრივი ფუნქციია ეკუთვნის იმ კლასის ობიექტს, რომელმაც აღწერა ის, მაგრამ arrow -ფუნქციებში არ გვაქვს default context, თუმცა შეგვიძლია ხელით bind,call ან apply.

3. **lexical scope** - განსაზღვრავს როგორ არის შესაძლებელი წვდომა ჩადგმულ ფუნქციებში, მაგალითად ყოველი შიდა ფუნქციას აქვს წვდომა მის გარე ფუნქციებზე მაგრამ პირიქით არა.

4. **Event loop** - როგორც ვიცით ჯს არის 1 სრედიანი, მაგრამ ბრაუზერი გვაძლევს საშუალებას რომ გავაკეთოთ async ფუნქციები პარალელურად ისე, რომ არ დაიბლოკოს მეინ სრედი. ნებისმიერი ასინქრონული ოპერაცია ბრაუზერის web api-ში მიდის, იმის მერე რაც დამუშავდება ვარდება ივენთების Queue-ში და როდესაც მორჩება ქოლ სტეკი მაშინ დაიწყება Queue-ში არსებული შედეგების დაბრუნება იმ თანმიმდევრობით როგორც ჩადგნენ. Call-Stack -> Web-Api -> Queue -> Call-Stack.

5. **Closure** - ეს არის ფუნქციის Scope-ში არსებული ობიექტი, სადაც ინახება ამ ფუნქციის ზედა ფუნქციაში(ებში) არსებული ცვლადები. როდესაც დაგვჭირდება ისინი ჯერ ვნახავთ თუ არსებობენ ქლოჟერში თუ არადა ზემოთ დაიწყება ძებნა ინიციალიზაციისთვის.

6. **Async/Await** - არის ES6-ის Keywords. Async ფუნქცია ყოველთვის აბრუნებს Promise-ს.
                                                     
                                                     async function f() {
                                                              return 1;
                                                     }
                                                     f().then(alert); // 1
   ხოლო await ელოდება მანამ სანამ არ მოვა let x = promise;
  7. **Promise** - არის კლასი რომელიც ასინქრონულ ფუნქციის მნიშვნელობას აბრუნებს როგორც სინქრონული ტიპი და პასუხისმგებელია დაბრუნების შემდეგ შედეგის, resolve ან reject.
  
  8. **Lifecycle Hooks** - 1. ანგულარის ციკლი იწყება ngOnChanges თუ არ ჩავთვლით კონსტრუქტორს, რომელიც არ არის ჰუკი და იტვირთება კლასის შექმნის თანავე, რათა მოხდეს საჭირო ინტერფეისების დაინჯექტება. ngOnChange-უზრუნველჰყოფს კომპონენტის დააფდეითებას მას შემდეგ რაც შეიცვლება მშობლის დატა, ის გამოიძახება ყოველთვის როცა კომპონენტში შემომავალი @Input() შეიცვლება, თუ კომპონენტში საერთოდ არ გვაქვს @Input()  არასდროს არ გამოიძახება ngOnChange. 
                       2. ამის შემდეგ მოდის ngOnInit-ი, რომელიც ერთხელ როდესაც მოხდება კომპონენტის ინიციალიზაცია,მისი ჩატვირთვის დროს უკვე ყველა დატა და პროპერტი დასეტილია. 
                       3. ამის შემდგომ მოდის ngDoCheck რომელიც იძახება ყველა ჩეინჯზე, ის ეშვება ყოველთვის ngOnChanges-გან განსხვავებით. მაგალითად თუ მე რაიმე შვილი კომპონენტი გადავიყვანე ChangeDetectionStrategy.OnPush-ზე, ანუ გავუთიშე default change detection, ანგულარი როგორ იქცევა - უყურებს მშობლის დატა, კერძოდ,თუ მშობლიდან მოწოდებული @Input() დატის რეფერენსი შეიცვლება, მაშინ დაიჭერს ამ ცვლილებას და გაეშვება ngOnChange-ი თუ არ შეიცვალა რეფერენსი - არ გაეშვება, ხოლო ngDoCheck-ი ყველაფრის და მიუხედევას დაიქოლება. ამიტომ, როდესაც ვთიშავთ ანგულარის default change detection-ს, რჩევა იქნება ის, რომ ვწეროთ immutable.js -თ, სადაც არ არსებობს mutable ობიექტები.
                       4. შემდეგ მოდის ngAfterContentInit, რომელიც ეშვება ერთადერთხელ როდესაც ყველა კონტენტი ჩაიტვირთება ამ კომპონენტის.  
                       5. ngAfterContentChecked - პირველად გამოიძახება ngAfterContentInit-ის მერე, მაგრამ ამის მერე ყოველი მცირე ჩეინჯზე ngDoCheck-ის მერე დაიქოლება.
                       6. ngAfterViewInit - დაიქოლება ერთადერთხელ, როცა წარმატებით ჩაიტვირთა ყველა შვილი კომპონენტი ngAfterContentChecked ამის შემდეგ.
                       7. ngAfterViewChecked - პირველად გამოიძახება ngAfterViewInit-ის მერე, მაგრამ ამის მერე ყოველ მცირე ჩეინჯზე ngDoCheck-ის მერე რიგში მოყვება ngAfterContentChecked-ს.
                       8. ngOnDestroy - გამოიძახება როდესაც კომპონენტი საჭიროებს წაშლას, მაგალითად კლიკზე გვინდა რომ გამოჩნდეს და გაქრეს კომპონენტი, როდესაც ვაქრობთ გამოიძახება ngOnDestroy.
  
  9. **როგორ მუშაობს ანგულარი** - დავუშვათ გვაქვს ერთი ესეთი პატარა კომპონენტი
  
                                                     \@Component({
                                                        selector: 'app-root',
                                                        templateUrl: `
                                                          <img src="cat.jpg">
                                                          <h1> {{header}} </h1>
                                                          <info-card [name]="name"></info-card>
                                                          <footer></footer>
                                                        `,
                                                        styleUrls: [ './app.component.css' ]
                                                      })
                                                      export class AppComponent  {...}\
     
       
       როდესაც ტაიპსკრიპტი კომპილირდება ჯს-ში, ასევე საჭიროა ანგულარის კოდი გადაითარგმნოს runtime-სთვის გასაგებ ენაზე. რას აკეთებს ანგულარის კომპილატორი ამისთვის, აიღებს ამ კომპონენტს და გადაწერს ასე, ამ ინსტრუქციებით:
                                                      
                                                      \AppComponent.ngComponentDef = defineComponent({
                                                          selectors:[['app-root']],
                                                          template: function(renderFlags,context){
                                                            if(renderFlags && renderFlags.Create){
                                                              element(0,'img',['src','cat.jpg']);
                                                              elementStart(1,'h1');
                                                              text(2);
                                                              elementEnd();
                                                              element(3,'info-card');
                                                              element(4,'footer');
                                                            }
                                                            if(renderFlags && renderFlags.Update)
                                                            {
                                                              advance(2);
                                                              textInterpolation1('',context.header,'');
                                                              advance(1);
                                                              property('name',context.name);
                                                            }
                                                          }
                                                      })/
     
                                              
  ამ ინსტრუქციებს კი უკვე runtime-ი დააიმპლემენტირებს. მოდი მოკლედ განვმარტოთ რა რას აკეთებს. ანგულარის კომპილატორი პირველ რიგში უყურებს ტემპლეიტს, რომელსაც გადაწერს ფუნქციის სახით,რომელსაც ფრეიმვორქი მიაწვდის იმის შესახებ ინფორმაციას ეს ტემპლეიტი იქმნება(renderFlags.Create) თუ აფდეითდება(renderFlags.Update); აი მაგალითად ამ შემთხვევაში ფრეიმვორქი აკეთებს ეგეთ რამეს: 
ჯერ გამოიძახებს მშობელი კომპონენტის template-ის create-ს : *App.ngComponentDef.template(create,app)*, შემდეგ უკვე *InfoCard.ngComponentDef.template(create,info)* და *Footer.ngComponentDef.template(create,footer)* 
template ფუნქციაში იყენებენ ანგულარის ფრეიმვორქის ინსტრუქციებს, რომლების თავისი აზრით იყოფა 2 სახის ინსტრუქციად:  Creation Instructions და Update Instructions. **Creation-ებია**: element() -რომელიც ქმნის ელემენტს,რომლის მაგალითსაც ქვემოთ დავწერ თუ როგორ მუშაობს,text(),template(),pipe(),listener() ... ხოლო **Update-ებია**: property(), attribute(),stypeProp(),pipeBind() და ა.შ.

მოდი დავწეროთ ერთ-ერთი ტემპლეიტის ინსტრუქცია element-ი როგორ მუშაობს.
                                                            
                                                            function element(index,tag,attrs){
                                                                const el = document.createElement(tag);
                                                                const parent = getCurrentParent();
                                                                setAttributes(el,attrs);
                                                                parent.appendChild(el);
                                                                const lView = getLView();
                                                                lView[index] = el;
                                                           }
 როგორც ვხედავთ ესაა ჩვეულებრივი plain js ფუნქცია, არაფერი განასკუთრებული.მოდი ვისაუბროთ რა არის lView და რატომ ვინახავთ კომპონენტის ელემენტს რაღაც კოკნკრეტულ ინდექსზე. ესეიგი, ჩვენ ვიცით რომ Change Detection-ზე ჩვენ დაგვჭირდება ესა თუ ის ელემენტი დავიჭიროთ და დავააფდეითოთ. რა თქმა უნდა შეგვიძლია DOM API გამოვიყენოთ და ისე ამოვიღოთ ეს ელემენტი, მაგრამ ეს საკმაოდ ძვირი ოპერაციაა, ამიტომ გვაქვს რაღაც ანგულარის შიდა სთორიჯი, რომელშიც კონკრეტულ ელემენტის ინდექსზე შევინახავთ ამ ელემენტს, ყოველ კომპონენტსს აქვს თავისი LView(Logical View). აი მაგალითად, ჩვენი კომპილატორის ინსტრუქციის მიხედვით lView arrya გამოიყურება ეგრე : 
                                                                                     [img,h1,txt,info-card,footer]
  
                                                                                     
  ეხლა როგორ არჩევს ანგულარი კონკრეტული ელემენტი დომის ელემენტია თუ ანგულარის. ჩვენ ვიცით რომ ანგულარის კომპონენტებს ინახავს registry:[InfoCard,Footer] ერეიში. ყოველ ჯერზე ამოწმებს ელემენტის სახელი ხომ არ ემთხვევა ამ რეგისტრიებიდან რომელიმეს თუ დაემთხვა მერე ქმნის უკვე მაგ კომპონენტის ტემპლეიტს. როგორ ინახება ეხლა ეს ერთიდაიგივე ტიპის კომპონენტების საერთო დირექტივები. მაგისთვის ანგულარი იყენებს TView(template view), სადაც ინახავს ყველა იმ დირექტივას რომელიც ჭირდება ამ კომპონენტის ინსტანსებს. ჩვენს შემთხვევაში TView გამოიყურება ასე, მოდი LView-სთან ერთად დავწერ რომ კარგად დავინახოთ : 
                                                                       LView  [img,h1,txt,info-card,footer]
                                                                       TView  [TNode,TNode,TNode,InfoCard.def,Footer.Def]
  LView ყველა ინსტანს აქვს თავისი, ხოლო TView არის 1 ყველა 1-ტიპის კომპონენტის ინსტანსისთვის.
  
  ზემოთ, დაკომპილირებულ ინსტრუქციაში ჩვენ უკვე აღვწერეთ როგორ გადაითარგმნა Update-ის ბრძანებები, ანუ Change Detection-ზე თუ რა უნდა მოხდეს. მოდი განვმარტოთ, რას ნიშნავს ეს ბრძანებები runtime-სთვის: *advance(2)* - ნიშნავს რომ LView-ში უნდა დავიძრათ 2 ბიჯით და მივადგეთ მე-3 ელემენტს ანუ მივედით txt-Node-თან, შემდეგ მოდის ბრძანება *textInterpolation1('',context.header,'');* რაც ააფდეითებს კლასის კონტექსის header-დან Value-ს, და ამავდროულად ქეშავს რომ თუ შეიცვალა დაქეშილს შეადაროს და მიხვდეს რომ Change Detection- გაუშვას, რასდგან შეიცვალა header-ცვლადი.ამის მერე ისევ *advance(1)* ბრძანება მოდის, ანუ მივადექით info-card-ს.რადგან ინფო-ქარდი არის ანგულარის კომპონენტი მისი ფროფერთის შესაცვლელად ვიყენებთ Update ინსტრუქციას, კერძოდ property მეთოდს რომელიც უშუალოდ იმ კომპონნენტში მიიტანს და შეცვლის Value-ს.
  
 

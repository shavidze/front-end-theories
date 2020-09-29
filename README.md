# all-about-javascript

1. **Hoisting, var, let, const, functions** - როდესაც ჯს ენჯაინი მიიღებს კოდს გასაშვებად, პირველ რიგში მემორიში გამოყოფს ადგილს, რომ შეინახოს ფუნცქციები და ცვლადები. ფუნქციები, როგორც წესი ინახები რეფერენსებად და დარეგისტრირებული ფუნქციის value ყოველთვის არის function-ი. რაც შეეხება ცვლადებს,es6-ს ახალი ტიპები let და const-ის ცვლადები ინახება, როგორც uninitialized , ხოლო var-ი ინახება როგორც undefined.
  
  
2. **context(this)** - ყველა ფუნქციას გააჩნია კონტექსტი, რომელიც მიუთითებს იმ ობიექტს რომელსაც ეკუთხვნის ეს ფუნქცია. როგორც წესი ჩვეულებრივი ფუნქციია ეკუთვნის იმ კლასის ობიექტს, რომელმაც აღწერა ის, მაგრამ arrow -ფუნქციებში არ გვაქვს default context, თუმცა შეგვიძლია ხელით bind,call ან apply.

3. **lexical scope** - განსაზღვრავს როგორ არის შესაძლებელი წვდომა ჩადგმულ ფუნქციებში, მაგალითად ყოველი შიდა ფუნქციას აქვს წვდომა მის გარე ფუნქციებზე მაგრამ პირიქით არა.

4. **Event loop** - როგორც ვიცით ჯს არის 1 სრედიანი, მაგრამ ბრაუზერი გვაძლევს საშუალებას რომ გავაკეთოთ async ფუნქციები პარალელურად ისე, რომ არ დაიბლოკოს მეინ სრედი. ნებისმიერი ასინქრონული ოპერაცია ბრაუზერის web api-ში მიდის, იმის მერე რაც დამუშავდება ვარდება ივენთების Queue-ში და როდესაც მორჩება ქოლ სტეკი მაშინ დაიწყება Queue-ში არსებული შედეგების დაბრუნება იმ თანმიმდევრობით როგორც ჩადგნენ. Call-Stack -> Web-Api -> Queue -> Call-Stack.

5. **Closure** - ეს არის ფუნქციის Scope-ში არსებული ობიექტი, სადაც ინახება ამ ფუნქციის ზედა ფუნქციაში(ებში) არსებული ცვლადები. როდესაც დაგვჭირდება ისინი ჯერ ვნახავთ თუ არსებობენ ქლოჟერში თუ არადა ზემოთ დაიწყება ძებნა ინიციალიზაციისთვის. პატარა მაგალითი:
                 
                function useState(){
                    let state = 0;

                    return function(increaseState){
                        state += increaseState;
                        console.log(state);
                    }
                }

                var st = useState();

                console.log(st(1)); // აქ დაბეჭდავს 1

                console.log(st(1)); // აქ დაბეჭდავს უკვე 2ს; 

                // რომ ჩავიხედოთ 2 რატომ დაბეჭდა 

                console.dir(st);

                // პირველ რიგში ნახულობს ეგეთი ცვლადი state უკვე ხომ არ აქვს ქლოჟერში შენახული, Scope -> Closure -> state და აგერ მანდ შეუნახავს.


6. **Async/Await** - არის ES6-ის Keywords. Async ფუნქცია ყოველთვის აბრუნებს Promise-ს.
                                                     
                                                     async function f() {
                                                              return 1;
                                                     }
                                                     f().then(alert); // 1
   ხოლო await ელოდება მანამ სანამ არ მოვა let x = promise;
  7. **Promise** - პრომისი ალბათ ის თემაა, რომელიც ყველაზე ცუდად არის ხოლმე ახსნილი ყველგან და ყოველთვის :). Promise არის ობიექტი, რომ გავხსნათ კონსოლი და დავბეჭდოთ **console.dir(new Promise(() => {} ));** დავინახავთ რომ მას აქვს 2 Property, პირველია [[PromiseStatus]] - სტატუსი, რომელსაც გააჩნია 3 მდგომარეობა, 3 value და [[PromiseValue]]. მოდით ავხსნათ რა value-ბი აქვს [[PromiseStatus]] და რას ნიშნავს თითოეული. fulfilled: ნიშნავს, რომ წარმატებით შესრულდა ყველაფერი, rejected: მოხდა რაღაც ერორი და დაარეჯექტდა და pending: ჯერ ველოდებით პასუხს, არც დარეზოლვებული და არც დარეჯექტებული. რაც შეეხება [[PromiseValue]] მას აქვს ორი მდგომარეობა undefined,როდესაც ჯერ არ დაბრუნებულა არაფერი, და შემდგომ უკვე ის რაც დაბრუნდება. ეხლა მოდი ავხსნათ ეს მდგომარეობები რის მიხედვით იცვლება. ზემოთ დაბეჭდილ პრომის, ჩვენ გავატანეთ arrow function , რომელიც არაფერს არ აკეთებს, მიუხედავათ ამისა,პრომისის callback ფუნქციას ზოგადად გადაეცემა ორი არგუმენტი, resolve და reject, რომელიც იმის მიხედვით გამოიძახება თუ როგორი წარმატებით დასსრულდა ქოლბექ ფუნქციია. მოდი უფრო ცხადი, რომ გახდეს დავწეროთ ეგეთი რამე</br> **console.dir(new Promise((resolve,reject) => resolve("completed")));**</br></br> დავინახავთ,რომ PromiseStatus - არის უკვე fullfiled (მიუხედავად იმისა რომ კონსოლში resolved ბეჭდავს,ეგ ბაგია ბრაუზერის), ხოლო PromiseValue : completed, ანალოგიურად იქნებოდა რომ დაგვებრუნებინა rejected("reject"), სტატუსი იქნებოდა  : "rejected" ,ხოლო value : "reject".</br> , რომ ჩავიხედოთ პრომისის prototype-ში, დავინახაავთ 3 built-in მეთოდს: then()-რომელიც გამოიძახება თუ Promese დარეზოლვდა, catch() - რომელიც გამოიძახება თუ დარეჯექტდა და finally() - რომელიც ყოველთვის გამოიძახება,მიუხედავად დაბრუნებული სტატუსისა. then() da catch() თვითონ აბრუნებენ Promise, რომელსაც ისევ შეგვიძლია callback-ი გავატანოთ,ანუ საშუალებას გვაძლევს მთელი ჯაჭვი ავაგოთ პრომისების.ეს იყო და ეს. </br></br> მოდი ივენთ ლუპში სად მიდის პრომისი მაგაზე ვთქვათ.როგორც ვიცით ასინქრონული ქოლები,რომელსაც ასაპორტებს ბრაუზერი მდიის ჯერ web api -> queue -> ხოლო როცა call stack მორჩება თანმიმდევრობით ბრუნდებიან. queue- თავისთავად იყოფა 2 ტიპის რიგად, პირველია  მაკროტასკების რიგი: setTimeOut, setInterval, setImediate ... , მეორეა მიკროტასკების: process.nextTick, Promise callback, async functions, queueMicrotask... როდესაც სტეკი დამთავრდება , რიგიდან ჯერ ეშვებიან მიკროტასკები და შემდეგ მაკროტასკები. ანუ პრომისი ყოველთვის უფრო ადრე დაბრუნდება რიგიდან ვიდრე setTimeOut :)).
  
  8. **Lifecycle Hooks** - 1. ანგულარის ციკლი იწყება ngOnChanges თუ არ ჩავთვლით კონსტრუქტორს, რომელიც არ არის ჰუკი და იტვირთება კლასის შექმნის თანავე, რათა მოხდეს საჭირო ინტერფეისების დაინჯექტება. როგორც ვიცით ნებისმიერი უმცირესი ცვლილება,რომელსაც ბრაუზერი უსმენს დავრაპული აქვს ანგულარის Change Detection-ს, რაც შეეხება ngOnChange-ს, ის იქოლება, მას შემდეგ რაც შეიცვლება მშობლის დატა შეიცვალა.ngOnChange - გამოიძახება ყოველთვის როცა კომპონენტში შემომავალი @Input() შეიცვლება,ხოლო თუ კომპონენტში საერთოდ არ გვაქვს @Input()  არასდროს არ გამოიძახება.</br></br>
                       2. ამის შემდეგ მოდის ngOnInit-ი, რომელიც ერთხელ როდესაც მოხდება კომპონენტის ინიციალიზაცია,მისი ჩატვირთვის დროს უკვე ყველა დატა და პროპერტი დასეტილია.</br></br>
                       3. ამის შემდგომ მოდის ngDoCheck რომელიც იძახება ყველა ჩეინჯზე, ის ეშვება ყოველთვის ngOnChanges-გან განსხვავებით. მაგალითად თუ მე რაიმე შვილი კომპონენტი გადავიყვანე ChangeDetectionStrategy.OnPush-ზე, ანუ გავუთიშე default change detection, სხვაგარად რომ ვთქვათ Change Detection Tree-დან detouch გავუკეთე ამ კომპონენტს რომ აღარ შეამოწმოს ყველა ჯერზე, ანგულარი როგორ იქცევა - უყურებს მშობლის დატა, კერძოდ,თუ მშობლიდან მოწოდებული @Input() დატის რეფერენსი შეიცვლება ან თუ პრიმიტიული თვითონ ამ პრიმიტიული ტიპის value, მაშინ დაიჭერს ამ ცვლილებას და გაეშვება ngOnChange-ი, ანუ მხოლოდ სტეკში შენახულ დატას ამოწმებს, ჰიპს არა, ხოლო ngDoCheck-ი ყველაფრის და მიუხედევას დაიქოლება. ამიტომ, როდესაც ვთიშავთ ანგულარის default change detection-ს, რჩევა იქნება ის, რომ ვწეროთ immutable.js -თ, სადაც არ არსებობს mutable ობიექტები. მოდი ცოტა მეტი ვისაუბროთ ანგულარის OnPush-ზე გადაყვანის მერე კიდევ რას თიშავს default detection. </br></br>
                       **ChangeDetectionStrategy.OnPush - მაინც უშვებს Change Detection-ს, თუ რაიმე დაატრიგერა დომის ივენთმა და ამ დროს სტეკში შეიცვალა რაიმე დატა,რომელიც მანამდე ყავდა დარეგისტრირებული ngOnChange-ში, და აი მაშინ გადაურბენს ყველაფერს რაც კი ყავდა ngOnChanges-ში დარეგისტრირებული და დააფდეითებს, იქნება ეს Object თუ პრიმიტივი. ასევე თუ ობზერვებლ დატასთან გამოვიყენებთ async პაიპს, ის იძახებს this.cdr.markForCheck-ს და უშვებს კომპონენტს ჩეინჯებზე შესამოწმებლად.**
                       **ChangeDetectionStrategy.OnPush - არ გაუშვებს ანგულარის დეტექშენს დომის აპიებზე, როგორიცაა setTimeOut და ა.შ**</br></br>
                       4. შემდეგ მოდის ngAfterContentInit, რომელიც ეშვება ერთადერთხელ როდესაც ყველა კონტენტი ჩაიტვირთება ამ კომპონენტის.  </br></br>
                       5. ngAfterContentChecked - პირველად გამოიძახება ngAfterContentInit-ის მერე, მაგრამ ამის მერე ყოველი მცირე ჩეინჯზე ngDoCheck-ის მერე დაიქოლება.</br></br>
                       6. ngAfterViewInit - დაიქოლება ერთადერთხელ, როცა წარმატებით ჩაიტვირთა ყველა შვილი კომპონენტი ngAfterContentChecked ამის შემდეგ.</br></br>
                       7. ngAfterViewChecked - პირველად გამოიძახება ngAfterViewInit-ის მერე, მაგრამ ამის მერე ყოველ მცირე ჩეინჯზე ngDoCheck-ის მერე რიგში მოყვება ngAfterContentChecked-ს.</br></br>
                       8. ngOnDestroy - გამოიძახება როდესაც კომპონენტი საჭიროებს წაშლას, მაგალითად კლიკზე გვინდა რომ გამოჩნდეს და გაქრეს კომპონენტი, როდესაც ვაქრობთ გამოიძახება ngOnDestroy.</br></br>
  
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
 როგორც ვხედავთ ესაა ჩვეულებრივი plain js ფუნქცია, არაფერი განასკუთრებული.მოდი ვისაუბროთ რა არის **lView** და რატომ ვინახავთ კომპონენტის ელემენტს რაღაც კოკნკრეტულ ინდექსზე. ესეიგი, ჩვენ ვიცით რომ Change Detection-ზე ჩვენ დაგვჭირდება ესა თუ ის ელემენტი დავიჭიროთ და დავააფდეითოთ. რა თქმა უნდა შეგვიძლია DOM API გამოვიყენოთ და ისე ამოვიღოთ ეს ელემენტი, მაგრამ ეს საკმაოდ ძვირი ოპერაციაა, ამიტომ გვაქვს რაღაც ანგულარის შიდა სთორიჯი, რომელშიც კონკრეტულ ელემენტის ინდექსზე შევინახავთ ამ ელემენტს, ყოველ კომპონენტსს აქვს თავისი **LView(Logical View)**. აი მაგალითად, ჩვენი კომპილატორის ინსტრუქციის მიხედვით lView arrya გამოიყურება ეგრე : 
                                                                                     [img,h1,txt,info-card,footer]
  
                                                                                     
  ეხლა როგორ არჩევს ანგულარი კონკრეტული ელემენტი დომის ელემენტია თუ ანგულარის. ჩვენ ვიცით რომ ანგულარის კომპონენტებს ინახავს registry:[InfoCard,Footer] ერეიში. ყოველ ჯერზე ამოწმებს ელემენტის სახელი ხომ არ ემთხვევა ამ რეგისტრიებიდან რომელიმეს თუ დაემთხვა მერე ქმნის უკვე მაგ კომპონენტის ტემპლეიტს. როგორ ინახება ეხლა ეს ერთიდაიგივე ტიპის კომპონენტების საერთო დირექტივები. მაგისთვის ანგულარი იყენებს **TView(template view)**, სადაც ინახავს ყველა იმ დირექტივას რომელიც ჭირდება ამ კომპონენტის ინსტანსებს. ჩვენს შემთხვევაში TView გამოიყურება ასე, მოდი LView-სთან ერთად დავწერ რომ კარგად დავინახოთ : 
                                                                       **LView**  [img,h1,txt,info-card,footer]
                                                                       **TView**  [TNode,TNode,TNode,InfoCard.def,Footer.Def]
  **LView** ყველა ინსტანს აქვს თავისი, ხოლო TView არის 1 ყველა 1-ტიპის კომპონენტის ინსტანსისთვის.
  
  ზემოთ, დაკომპილირებულ ინსტრუქციაში ჩვენ უკვე აღვწერეთ როგორ გადაითარგმნა Update-ის ბრძანებები, ანუ Change Detection-ზე თუ რა უნდა მოხდეს. მოდი განვმარტოთ, რას ნიშნავს ეს ბრძანებები runtime-სთვის: *advance(2)* - ნიშნავს რომ LView-ში უნდა დავიძრათ 2 ბიჯით და მივადგეთ მე-3 ელემენტს ანუ მივედით txt-Node-თან, შემდეგ მოდის ბრძანება *textInterpolation1('',context.header,'');* რაც ააფდეითებს კლასის კონტექსის header-დან Value-ს, და ამავდროულად ქეშავს რომ თუ შეიცვალა დაქეშილს შეადაროს და მიხვდეს რომ Change Detection- გაუშვას, რასდგან შეიცვალა header-ცვლადი.ამის მერე ისევ *advance(1)* ბრძანება მოდის, ანუ მივადექით info-card-ს.რადგან ინფო-ქარდი არის ანგულარის კომპონენტი მისი ფროფერთის შესაცვლელად ვიყენებთ Update ინსტრუქციას, კერძოდ property მეთოდს რომელიც უშუალოდ იმ კომპონნენტში მიიტანს და შეცვლის Value-ს.
  
 10. **Types Everywhere** - როდესაც ჩვენ ტიპიზირებას ვუკეთებთ ფუნქციებს და პარამეტრებს, ერორი ხდება კომპაილ ტაიმში. რა ხდება თუ ჩვენ არ ვუთითებთ ტიპებს ჯს-ში? დავუშვათ, გვაქვს რაღაც ფუნქცია 
 
                                    function(a,b){
                                      return a+b;
                                    }
 კომპაილში ეს ფუნქცია ჩვეულებრივად გაივლის,არ გავა ერორზე,გადაითარგმნება engine-სთვის გასაგებ ენაზე და უკვე იქ დაიწყება გარკვევა რა ტიპები არიან ეს პარამეტრები და უკვე ამ კონკრეტული პარამეტრებისთვის ენჯინი დაარეზერვებს ფუნქციას თუ როგორ უნდა შეკრიბოს ეს 2 ცვლადი, ასეთ დარეზერვებულ ფუნქციებს ეძახიან monomorphic ფუნქციებს. ეხლა ეს დარეზერვება რატომ უნდა თუ შემდეგ ჯერზე იგივე ტიპები მოვიდა ,უკვე მიადგება ამ დარეეზერვებულ ფუნქციას და ძალიან შეამცირებს გაშვების დროს. თუ რომელიღაც ჯერზე, რომელიმე ინფუთ პარამეტრმა შეიცვალა ტაიპი, engine-ი წაშლის ამ დარეზერვებულ ფუნქციას და ახლიდან დაწერს როგორ უნდა შეკრიბოს ეს ტიპები და ეხლა უკვე ამ ფუნქციას დაარეზერვებს, ალბათ ხვდებით რომ ეს არაა ეფექტური. ამიტომ როდესც, ჩვენ ვიყენებთ ტიპიზირებას, არამარტო დებაგი გვიალდიდება, და კომპაილში ერორების დაჭერა არამედ ყოველთვის ერთი და იგივე დარეზერვებულ ფუნქციას მიადგება engine და ეფექტურად გამოთვლის ფუნქციის პასუხს.

11.  **Pure and Impure Pipes** - როგორც ვიცით პაიპები გვჭირდება დატის ტრანსფორმაციითვი,ს default-ად ჩვენ ვიყენებთ *Pure* პაიპებს, რაც აკეთებს მემოიზაციას,რაც ნიშნავს იმას რომ თუ კონკრეტული პრიმიტიული რიცხვისთვის ან რეფერენსისთვის გამოთვლილი გვაქვს შედეგი ამ შედეგს (რომელიც ოდესღაც დაითვალა და ქონდა state-ში შენახული) დააბრუნებს, ხოლო Impure-ს დროს ყოველთვის შემოვა და თავიდან გააკეთებს კალკულაციას.

12. **Single Pattern in angular** - ანგულარი იყენებს სინგლტონ პატერნს, კერძოდ როდესაც ჩვენ ვქმნით სერვის და ვაინჯეტებთ რუთში, იქმნება 1 ინსტანსი სერვისის და ყველა აინჯექტებს ამ კონკრეტულ ინსტანს.

13. **RXJS** - 1.map - გამოიყენება რომ ობსერვებლში შემომავალ ივენთებს მოვდოთ ფუნქცია და დავაბრუნოთ ახალი სტრიმი.
               2.flatMap - იგივე მეპი, უბრალოდ აქ უეჭველად ვიცით რომ 1 ობსერვებლი დაბრუნდება სადაც თითოეული ივენთი იქნება value და არა ობსერვებლი
               3. mergeMap - არის map-ის და mergeAll-ის გაერთიანება, კერძოდ თუ გვაქვს რაიმე სტრიმი, რომლის თითოეულ ივენთის value-ს მოვდოთ რაიმე ფუქნცია, რომელიც თავისთავადა დააბრუნებს სტრიმს და ჩვენ საბოლოოდ ამ ყველა დაბრუნებული სტრიმების 1 სტრიმში გაერთიანება გვინდა , მაგისთვის ვიყენებთ mergeMap-ს.სტრიმებში ივენთების მოსვლის თანმიმდევრობა დაცულია.
               
                // using a regular map
                from([1,2,3,4]).pipe(
                  map(param => getData(param))
                ).subscribe(val => val.subscribe(data => console.log(data)));

                // using map and mergeAll
                from([1,2,3,4]).pipe(
                  map(param => getData(param)),
                  mergeAll()
                ).subscribe(val => console.log(val));

                // using mergeMap
                from([1,2,3,4]).pipe(
                  mergeMap(param => getData(param))
                ).subscribe(val => console.log(val));/
       4.switchMap - აქანსელებს შიდა ჩადგმულ ობზერვებლს, როდესაც ახალი ივენთი დაემიტტება გარე ობზერვებლში.
       5.concatMap - იგივეა რაც mergeMap, ერთი განსხვავებით სანამ მიმდინარე observable-ს  შესრულება შემდეგს არ დაასაბსქრაიბებს.
14. **Observables** — 1. Subject - არის ჩვეულებრივი ობზერვებლი, რომელსაც შეგვიძლია დავუერთოთ მრავალი ობზერვერები.
                     2. Behaviour Subject - იგივეა რაც Subject,ერთი განსხვავებით რომ როდესაც მეორე ობზერვერი შემოუერთდება ბოლო დაემიტებულ Value რომლის დაჭერა ვერ მოასწრო იმასაც დაუემიტებს.
                     3. Reply Subject - იგივე Behaviour Subject, ერთი განსხვავებით რომ როდესაც მეორე ობზერვეი შემოუერთდება ყველა მაქამდე არსებულ Value რომლის დაჭერა ვერ მოასწრო იმასაც დაუემიტებს.
                     4. Async Subject - გაატარებს ყველა Values , მხოლოდ გაატანს ბოლოს ობზერვერებისთვის.
15. **Zone.js** — zone-არის execution context, რომელიც საშუალებას გვაძლევს დავრაპოთ ორიგინალი ასინქრონული ფუნქციები და სანამ ორიგინალი გაეშვება მანამდე და მაგის მერეც რაიმე კოდი დავაგენერიროთ. უფრო კარგად, რომ დავინახოთ: 
                       
                       var Zone = {
                            run: function (callback) {
                                if (this.beforeTask) {
                                    this.beforeTask();
                                }
                                callback();

                                if (this.afterTask) {
                                    this.afterTask();
                                }
                            }
                        }

                        Zone.beforeTask = () => { console.log("BEFORE TASK") }

                        Zone.afterTask = () => { console.log("AFTER TASK") }

                        //Zone.run(() => { console.log("HELLO ZONE") })


                        // დავრაპოთ ორიგინალი setTimeout

                        var _setTimeout = setTimeout;

                        setTimeout = (callback, timeout) => {
                            Zone.run(() => {
                                _setTimeout(callback, timeout);
                            })
                        }

                       setTimeout(() => console.log("Set Time Out is running"), 1000);
     ანგულარი იყენებს zone.js ,დავრაპული აქვს ყველა ასინქრონული ფუნქცია და zone-ში უშვებს, ამ ფუნქციებს და შემდეგ კი უკვე ჩეინჯ დეტექშენს აღძრავს, რათა გაიგოს თუკი რაიმე შეიცვალა რომ დომი დააფდეითოს. მარტივად შეგიძლიათ ნახოთ, რომ main.ts-ფაილში თუ გავითიშავთ ng-zones, *platformBrowserDynamic().bootstrapModule(AppModule,[{ngZone:'noop'}]).catch(err => console.error(err))*-ასე, ვნახავთ რომ სულ მცირე დომის ივენთზეც კი, მაგალითად კლიკზე გვინდა გავზარდოთ ცვლადი და დომში დავააფდეითოთ, დავინახავთ რომ ცვლადი გაიზრდება მაგრამ დომში არაფერი არ მოხდება, რადგან ჩეინჯ დეტექშენზე გაშვებას აკეთებს zone.js რომელიც გავთიშეთ.

16. **Decorators in Typescript** — ტაიპსკრიპტმა ექსპერიმენტების ფარგლებში წარადგინა ახალი feature, დეკორატორები, რომელიც მსგავსია C#,Swift - attribute ტეგების. დეკორატორები არიან ფუნქციები რომელიც ეშვებიან runtime-ში, ხოლო არგუმენტად იღებენ იმ გამოსახულებას რომელიც მოსდევთ აღწერის შემდეგ: კლასები,მეთოდები,პარამეტრები თუ უბრალოდ property-ები.
                                    
                                    function LogClass(constructor: Function) {
                                        console.log('LogClass decorator executed for the constructor:');
                                        console.log("class =", constructor);

                                        console.log("-------------------")
                                   }
     @LogClass რომ მოვდოთ რაიმე ts კლასს, მიიღებს ამ კლასს პარამეტრად და დაბეჭდავს. შეგვიძლია პარამეტრიანი ფუნქცია გვქონდეს და ის აბრუნებდეს ფუნქციას რომელსაც მოვდეთ პარამეტრად კლასი, მაგალითად ასე.
                                    
                                    function LogClassWithParams(pref: string, suff: string) {
                                      return (constructor: Function) => {
                                        console.log(`${pref}\n\n Class decorator called for: ${constructor}\n\n ${suff}`)
                                        console.log("-------------------")
                                      }
                                    }
რა თქმა უნდა, არ ვართ შეზღუდულები რაოდენობაში, ჩვენ შეგვიძლია ერთ კლასს მოვდოთ რამდენიმე დეკორატორი, რომლებიც გაეშვებიან მარცხნიდან მარჯნივ.

17. **JIT & AOT** — *Jit* არის run-time compilation, როცა გაშვებისას ხდება კოდის კომპილაცია და მანქანურ ენაზე გადათარგმნა. 
                    *AOT* არის ისეთი კომპილაციის პროცესი, როდესაც ჯერ build-ის ხდოს ხდება კომპილაცია, მანქანურ ენაზე ინსტრუქციების გაწერა და შემდგომ უკვე მოაქვს სერვერიდან კოდი ბრაუზერს და უშვებს.ეს გაცილებით სწრაფია ვიდრე JIT, რადგანაც აქ უკვე გვაქვს წინასწარ დაკომპილირებული კოდი და როდესაც ხდება რენდერი აღარ ველოდებით თავიდან კომპილაციას.ასევე გარე HTML/CSS-ებს ჯს-ში ტენის და აღარ ჭირდება ცალკე ajax რექვესტები, რომ წამოიღოს ეს ფაილები.ერორებს გაშვებამდე იჭერს და არის უფრო მეტად დაცული.

18. **Typescript** - აქ განვიხილითოთ რამდენიმე საჭირო utility types ტაიპსკრიპტის. *Partial<T>* - ეს იგივეა რომ ნებისმიიერი T ინტერფეისის პროპერტიები იყოს nullable , *ReadOnly<T>* მხოლოდ წაკითხვადს გახდის. მოდი მაგალითის საფუძველზე განვიხილოთ Record<T,K>. დავუშვათ გვაქვს ინტერფეისი PageInfo { title: string } და type Page = 'home' | 'about' | 'contact'. თითოეული ტიპისგან შევადგინოთ ინტერფეისი, სადაც თითოეულისთვის T-დან ტიპი იქნება K ტიპის.
  const x: Record<Page, PageInfo> = {
    about: { title: 'about' },
    contact: { title: 'contact' },
    home: { title: 'home' },
};
*Pick<T,K>* - T ინტერფეისიდან ამოიღებს K -ს ტიპის პროპერტიებს და დააბრუნებს ახალ ინტერფეის.
 *Omit<T,K>* - T ინტერფეისიდან ამოშლის K-s ტიპის პროპერტიებს და დააბრუნებს ახალ ინტერფეის.
 *Exclude<T,K>* - დააბრუნებს ყველა T-ტიპს გარდა K-ს ტიპებისა.
  
  
 *ჯენერიკ ტიპები* : type Container<T> = { value: T };
 *გრაფისნაირი სტრუქტურის ტიპიზირება* : 
      type Tree<T> = {
        value: T;
        left: Tree<T>;
        right: Tree<T>;
      }
 *LinkedIn-ის სტრუქტურე*: type LinkedIn<T> = T & { next: LinkedIn<T> };
  
  ერთადერთი მნიშვნელოვანი სხვაობა type alias და interface შორის არის ის რომ type alias-ით შეგვიძლია union,intersect და სხვადასხვა ფუნცქიების გამოყენები, მაგრამ არ შეგვიძლია ერთი და იგივე ტიპის ორჯერ განსაზღვრა, რაც ინტერფეისით შეგვიძლია, მაგალითად interface P { x: number} რომ განსვსაზღვროთ მეორედ და დავწეროთ interface P {y:number} საბოლოოდ იქნება interface P {x :number, y: number} რაც არ შეიძლება ტაიპებზე. 
  
*ახალი ტიპის გამოდგმა(სიტყვაზე რომელიც TInterface -დან არსებულ ტიპებს გახდის მასივებს)* : type X  = {
                            [K in keyof TInterface]: TInterface[K][]
                          }
  

19. **CORS** - ფრონტიდან რაღაც დატა ყოველთვის მოგვაქვს რაღაც სერვერიდან , რომელსაც ვწვდებით კონკრეტული დომეინით. ფრონტს ყოველთვის შეუძლია მაგ სერვერზე გაუშვას რაღაც ვირუსები და ა.შ. მაგისგან თავის დასაცავად ბრაუზერს აქვს *same-origin policy*, რომელიც ამოწმებ იმას თუ რომელი დომეინიდან რომელ დომეინზე მოდის რესპონსი( დავაკვირდეთ აქ იმას რომ თვითონ რექვესტი იგზავნება, იქიდანაც მოდის რესპონსი მაგრამ უკვე ბრაუზერი ამოწმებს საიდან მოდის და ემთხვევა თუ არა თავის ორიგინალს საიდანაც გაუშვეს რექვესტი), თუ ისინი არის განსხვავებული. ეხლა განსხვავებული რას ეწოდება მაგალითად გვაქვს https://www.web.com, Same Origin -იქნება http://www.web.com/page ,მაგრამ განსხვავებულები არიან უკვე https:://www.api.web.com ან თუ სხვა პროტოკოლი აქვს http - ი მაგალითად, ან თუ სხვა პორტი აქვს და ა.შ. როგორ შეილება ვაკომუნიკაციოთ ეხლა მოგვარდეს , ამისთვის სერვერის მხრიდან რესპონსში გავუწერთ "Access-Control-Allow-Origin", "https://anotherweb.com", რადგან ფრონტიდან ვიცით რომ HTTP რექვესტs ჰედერებში მოყვება ეგეთი meta tag Origin: "https://web.com" ანუ საიდან მიდის რექვესტი, სერვერის მხრიდან დაბრუნებულ დაშვებულ ორიჯინს შეაადარებს ბრაუზერი, თუ აქვს უფლება გაწერილი სერვერიდან მაშინ მიცემს უფლებას რომ აიღოს ფრონტმა. სერვერსი მხრიდან ასევე შეგვიძლია შევზღუდოთ მეთოდებით წვდომა Access-Control-Allow-Methods თუ რა მეთოდებზე აჩვენოს რესპონსი ბრაუზერმა. მოდი უფრა დაწვრილებით გავარჩიოთ როგორ ხდება ეს ყველაფერი. სანამ უშუალოდ რექვესტი გაეშვება, მანამდე ეშვება Preflighted Request.
        
       Actual Requsest : PUT https://api.web.com/user/1  HTTP/1.1
                         Origin: https://web.com
                         Content-Type: application/json
       
       Preflighted Request: Options htps://api.web.com/user/1 HTTP/1.1
                            Origin: https://www.web.com
                            Acces-Control-Request-Method: PUT
                            Access-Control-Request-Headers: Content-Type
                            
   ესაა განსხხავვება , მათ შორის. ეხლა რადგან ჯერ მიდის Preflighted Request , სერვერი იღებს ამას და ისიც აბრუნებს Preflighted Response 
        Prefilted Response: HTTP/1.1 204 No Content
                            Access-Control-Allow-Origin: https://www.web.com
                            Access-Control-Alow-Methods: GET POST PUT
                            Date : ...
                            Server: ...
  
  ეს უბრუნდება ბრაუზერს, რომელსაც გარშემო არტყავს ქორსი, რომელმაც უნდა შეამოწმოს დაბრუნებული და გაგზავნილი Preflighted Request/Response რამდენად რთავს უფლებას გაუშვას აქტუალური რექვესტი.



20. 
  **useClass** - მოდი ცოტა გავშალოთ DI-ს თემა, როდესაც ჩვენ პროვაიდერებში ვარეგისტრირებთ კლასის სახელს, და შემდეგ უკვე ვცდილობთ ამ კლასის სახელით კონსტრუქტორში მივიღოთ ეს სერვის კლასი , ანგულარი აკეთებს ეგეთ რამეს: 
     ეს providers: [MyService] გადაიწერება ასე 
        providers: [ 
              {
                provide: MyService,
                useClass: Myservice,
               }
         ]
  ანუ რა გამოდის რომ ანგულარი ამ კლასის სახელის ტოკენზე არეგისტრირებს თავად ამ კლასს, ანუ გამოდის რომ ჩვენ მარტივად შეგვიძლია მაგ კლასის სახელზე სხვა კლასი გავწეროთ useClass - ში და უკვე სადაც დაველოდებით MyService მოვა სხვა კლასი რრასაც დავურეგისტრირებთ useClass: OtherService - ს მაგალითად.
  **useValue** - მოდი განვიხილოთ ეს feature. ზოგჯერ გვსურს რომ კონსტრუქტორში მივიტანოთ დინამიურად არა რომელიმე სერვისი, არამედ რაიმე ობიექტი ან value, ზოგადად რომ ვთქვათ DI-ze , ეს არის მექანიზმი როცა ვიღაცას სურს რაღაცა დაირეგისტრიროს, მაგალითად კოსტრუქტორში ვიღაც ტიპს სურს myService იყოს, ან უბრალოდ რაიმე ობიექტი. მაგალითად გვაქვს რაღაც ობიექტი :
    let myObject = { greeting: 'Hello DI!' }; და ეხლა ვარეგისტრირებთ ამ ობიექტს 
    providers : [ 
         {
            provide: 'MyService' // აქ ჯობს უბრალოდ სტრინგზე დავარეგისტრიროთ ვიდრე რაიმე კლასზე 
            useValue: myObject
         }
    ]
    და უბრალოდ constructor(@Inject('MyService') myService) ასე დავარეგისტრირებთ ამ ტოკენით და რომ ჩავხედოთ უკვე myService.greeting იქნება 'Hello DI'.
    
   **useFactory** - ეს არის რაღაც ფუნქცია რის მიხედვითაც მოცემულ ტოკენზე დავრეგისტრირებთ რაიმე ლოგიკით VALUE-ს.
  განსაკუთრებული არაფერი უბრალოდ ფუნქციაა და არა პირდაპირ useValue.
  
  ერთადერთი პრობლემა რასაც ვაწყდებით ხოლმე არის სახელების დამთხვევა ანუ collision , როცა ხან სტრინგად და ხან კლასად ვურეგისტრირებთ რაიმე ერთი და იმავე სახელს. ამის მარტივად მოსაგვარებლად ანგულარს აქვს InjectionToken რომელიც აბრუნებს ტოკენს და ამასთან ყველა ახალი ინსტანსი ამ კლასის არის განსხვავებული და არასდროს გვექნება ეს collision.
  const NewToken = new InjectionToken<MyInterface>('token description');
  
  ყველაზე განსაკუთრებული feature მაინც არის მოდულისთვის დინამიურად დაგენერირებული პროვაიდერები. მაგალითად როდესაც ჩვენ ვწერთ რაიმე სერვის რომელსაც გარედან სჭირდება რაღაც config-ების გადმოცემა , რომ იყოს ჯენერიკი და შეძლოს ყველამ გამოიყენოს. მაგალითად მოდულში გვაქვს სერვისი რომელსაც სჭირდება ეგეთი config { spaceId, contentId } , რომელსაც უზერი გამოიყენებს დდინამიურად როცა რა დაჭირდება იმას გაატანს. ეს რომ სტატიკურად გვქონდეს უკვე დაიკარგება ლაიბრერად გამოყენების თემა. ამიტომ შეგვიძლია 
  forRoot - ში დავარეგისტრიროთ გარედან რაც გვინდა .
    const ContentfulConfigService = new InjectionToken<ContentfulConfig>("ContentfulConfig");//ConterfullConfig - ინტერფეისია უბრალოდ
    @NgModule()
      export class ContentfulModule {
        static forRoot(config: ContentfulConfig): ModuleWithProviders {
          return {
            ngModule: ContentfulModule,
            providers: [
              ContentfulService,
              {
                provide: ContentfulConfigService,
                useValue: config
              }
            ]
          }
        }
      }
    
  და სადაც გამოვიყენებთ ამ მოდულს იქიდან გამოვატანს ამ კონფიგსაც. 
  const contentfulConfig: ContentfulConfig = { 
    spaceId: 'YOUR-SPACE-ID',
    accessToken: 'YOUR-TOKEN'
  }
  ContentfulModule.forRoot(contentfulConfig) აი ასე. რაც შეეხება გამოყენებას: 
  
  ეს ContentfulService კონსტრუქტორში მიიღებს ამ config-ს :
  
  constructor(@Inject(ContentfulConfigService) private config)
  
  ანუ ამ config - ექნება spaceId-ც და contentId-ც.
  //https://stackblitz.com/edit/angular-contentful-medium
  
  
  
      
      



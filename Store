<?php
ob_start();
$API_KEY = 'توكن';
define('API_KEY',$API_KEY);
function bot($method,$datas=[]){
$url = "https://api.telegram.org/bot".API_KEY."/".$method;
$ch = curl_init();
curl_setopt($ch,CURLOPT_URL,$url);
curl_setopt($ch,CURLOPT_RETURNTRANSFER,true);
curl_setopt($ch,CURLOPT_POSTFIELDS,$datas);
$res = curl_exec($ch);
if(curl_error($ch)){
var_dump(curl_error($ch));
}else{
return json_decode($res);
}
}
$update = json_decode(file_get_contents('php://input'));
$message = $update->message;
$text = $update->message->text;
$chat_id = $update->message->chat->id;
$from_id = $update->message->from->id;
$message_id = $update->message->message_id;
$id = $update->inline_query->from->id; 
$text_inline = $update->inline_query->query;
$users = explode("\n", file_get_contents("users.txt"));
if($text_inline){
bot('answerInlineQuery',[
'inline_query_id'=>$update->inline_query->id,    
'results' => json_encode([[
'type'=>'article',
'id'=>base64_encode(rand(5,555)),
'title'=>'ارسال الكليشة 💌',
'input_message_content'=>[
'parse_mode'=>'markdown',
'disable_web_page_preview'=>true,
'message_text'=>"
- مرحبا بكم في بوت الماركت 🛍 •

- البوت الاكبر ع تليجرام 📊 •

- يوجد داخله اقسام اكثر استفادة 📌 •

- يمكنك شراء اي شي مجاناً ملاً ⏬ •
(حسابات - بوتات - تمويل - سيرفرات *vps* - لخ...)

- كل ما عليك هوه دخول الى رابط هنا ⏬ •
"],
'reply_markup'=>[
'inline_keyboard'=>[
[['text'=>'بوت ماركت 🛍','url'=>"https://t.me/TPstoreBot?start=$id"]],
]]]])]);}
//____________________________________________________
$sudo = "ايدي المطور";
$yes = file_get_contents("ok.txt");
$sudobot = "معرف المطور بدون @";
$channel1 = "معرف القناة";
$channel2 = file_get_contents("ch.txt");
//____________________________________________________
if(isset($update->callback_query)){
$callbackMessage = '';
var_dump(bot('answerCallbackQuery',[
'callback_query_id'=>$update->callback_query->id,
'text'=>$callbackMessage]));
$chat_id = $update->callback_query->message->chat->id;
$from_id = $update->callback_query->from->id;
$user = $update->callback_query->from->username;
$message_id = $update->callback_query->message->message_id;
$data = $update->callback_query->data;
}
$link = explode(" ", $text);
$get = file_get_contents("data/$from_id.txt");
$put = 10;
if($link[0] == "/start" and !in_array($chat_id, $users)){
$k = file_get_contents("data/$link[1].txt");
$yes = $k + $put;
file_put_contents("data/$link[1].txt", $yes);
bot("sendmessage",[
'chat_id'=>"$link[1]",
'text'=>"
- دخل شخص بـ أستخدام رابط دعوة خاص بك 🖇 •
- ربحت 10 نقاط وتم اضافة الى رصيدك 📌 •
",
]);
}
if($link == "/start" and $from_id == $link[1]){
bot('sendmessage',[
'chat_id'=>$chat_id,
'text'=>"- لا يمكن دخول ع رابط الخاص بك 🚫 •",
]);
}
if(!in_array($chat_id, $users)){ 
file_put_contents("users.txt",$chat_id."\n", FILE_APPEND);
}
$ch1 = file_get_contents("https://api.telegram.org/bot".$API_KEY."/getChatMember?chat_id=$channel1&user_id=".$from_id);
$ch2 = file_get_contents("https://api.telegram.org/bot".$API_KEY."/getChatMember?chat_id=$channel2&user_id=".$from_id);
$json1 = json_decode(file_get_contents("http://api.telegram.org/bot".$API_KEY."/getChat?chat_id=$channel1"))->result;
$json2 = json_decode(file_get_contents("http://api.telegram.org/bot".$API_KEY."/getChat?chat_id=$channel2"))->result;
$ch_user1 = $json1->username; 
$ch_user2 = $json2->username; 
$ch_name1 = $json1->title;  
$ch_name2 = $json2->title;  
if(strpos($ch1 , '"status":"left"') !== false and strpos($ch2 , '"status":"left"') !== false or !strpos($ch1 , '"status":"left"') !== false and strpos($ch2 , '"status":"left"') !== false or strpos($ch1 , '"status":"left"') !== false and !strpos($ch2 , '"status":"left"') !== false){
bot('sendMessage',[
'chat_id'=>$chat_id,
'parse_mode'=>'Markdown',
'text'=>"
- اشترك في قنوات البوت اولا 😻🎩 •
- اذا لم تشترك في قنوات البوت 👁‍🗨 •
- البوت لم يعمل اشترك ورجع ارسل امر (/start) 🌹 •
",
'reply_markup'=>json_encode([
'inline_keyboard'=>[
[['text'=>"$ch_name1", 'url'=>"https://telegram.me/$ch_user1"]],
[['text'=>"$ch_name2", 'url'=>"https://telegram.me/$ch_user2"]],
]])
]);
}
if(!strpos($ch1 , '"status":"left"') !== false and !strpos($ch2 , '"status":"left"') !== false){
if($data == "🔙"){
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"
- مرحبا بك في بوت الماركت المتنوع 😻🎩 •
- البوت يجمع اكبر عدد من المبيعات بارخص الاسعار ✨ •
- يمكنك جمع رصيد برابط دعوة 🔗 •
- او يمكنك شراء رصيد في البوت وشراء الي شي من خلال رصيدك 📍•
", 
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"معرفة الرصيد",'callback_data'=>"q"]],
[['text'=>"قسم التمويل",'callback_data'=>"w"],['text'=>"قسم البوتات",'callback_data'=>"e"]],
[['text'=>"قسم الحسابات",'callback_data'=>"r"],['text'=>"قسم اليوزرات",'callback_data'=>"t"]],
[['text'=>"شراء نقاط",'callback_data'=>"stor"],['text'=>"صنع رابط دعوة",'callback_data'=>"link"]],
]])
]);
}
if($link[0] == "/start" and $from_id != $link[1]){
bot('sendMessage',[
'chat_id'=>$chat_id, 
'text'=>"
- مرحبا بك في بوت الماركت المتنوع 😻🎩 •
- البوت يجمع اكبر عدد من المبيعات بارخص الاسعار ✨ •
- يمكنك جمع رصيد برابط دعوة 🔗 •
- او يمكنك شراء رصيد في البوت وشراء الي شي من خلال رصيدك 📍•
", 
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"معرفة الرصيد",'callback_data'=>"q"]],
[['text'=>"قسم التمويل",'callback_data'=>"w"],['text'=>"قسم البوتات",'callback_data'=>"e"]],
[['text'=>"قسم الحسابات",'callback_data'=>"r"],['text'=>"قسم اليوزرات",'callback_data'=>"t"]],
[['text'=>"شراء نقاط",'callback_data'=>"stor"],['text'=>"صنع رابط دعوة",'callback_data'=>"link"]],
]])
]);
}
if($data == "link" ){
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"
- كيف تجمع نقاط مجاناً طريقة سهلة كلش 📌 •

- يوجد نوعين من حصول ع نقاط مجاناً تابع...♻️ •

- (1) تنسخ رابط وتقوم بنشره ✔️ •

- (2) تقوم بضغط ع زر الشفاف ونشره معه كليشة ☑️ •

- يفضل نشر معه كليشة لضمان ربح نقاط 💯 •

كل شخص يقوم بدخول الى البوت رابط دعوة خاص بك تربح 10 نقاط❗️•

- رابط دعوة الخاص بك ⏬ •

- https://t.me/TPstoreBot?start=$from_id •

- لنشر معة كليشة اضغط هنا ⏬ •
", 
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>'شارك الرابط دعوة خاص بك 🖇', 'switch_inline_query'=>"$from_id"]],
[['text'=>"رجوع",'callback_data'=>"🔙"]],
]])
]);
}
// قسم معرفة الرصيد
if($data == "q"){
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"
- رصيد حسابك هو :: $get ☑️ •
", 
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"رجوع",'callback_data'=>"🔙"]],
]])
]);
}
// قسم التمويل
if($data == "w"){
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"
- تمويل كروب 50 عضو بـ500 👁‍🗨 •

- تمويل كروب 100 عضو بـ900 👁‍🗨 •

- تمويل قناة 100 عضو بـ400 👁‍🗨 •

- تمويل قناة 200 عضو بـ800 👁‍🗨 •

- تمويل القناة 300 عضو بـ1200 👁‍🗨 •

- تمويل القناة 400 عضو بـ1600 👁‍🗨 •

- تمويل قناة 500 عضو بـ2000 👁‍🗨 •
", 
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء 50 عضو الى كروبك",'callback_data'=>"gp50"]],
[['text'=>"شراء 100 عضو الى كروبك",'callback_data'=>"gp100"],['text'=>"شراء 100 عضو الى قناة",'callback_data'=>"ch100"]],
[['text'=>"شراء 200 عضو الى قناة",'callback_data'=>"ch200"],['text'=>"شراء 300 عضو الى قناة",'callback_data'=>"ch300"]],
[['text'=>"شراء 400 عضو الى قناة",'callback_data'=>"ch400"],['text'=>"شراء 500 عضو الى قناة",'callback_data'=>"ch500"]],
[['text'=>"رجوع",'callback_data'=>"🔙"]],
]])
]);
}
if($data == "gp50" and $get >= 500){
file_put_contents("$from_id.txt", "gp50");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل رابط كروبك لا غير ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "gp50" and $get <= 500){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"w"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "gp50"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 500 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 500;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء 50 عضو الى كروب 🔝 •
- رابط الكروب ↙️ •
$text",
]);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء 50 عضو الى كروب 🔝 •
- رابط الكروب ↙️ •
$text",
]);
}
if($data == "gp100" and $get >= 900){
file_put_contents("$from_id.txt", "gp100");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل رابط كروبك لا غير ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "gp100" and $get <= 900){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"w"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "gp100"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 900 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 900;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sud,
"text"=>"- طلب احد الاشخاص شراء 100 عضو الى كروب 🔝 •
- رابط الكروب ↙️ •
$text",
]);
bot("sendmessage",[
"chat_id"=>$sud,
"text"=>"- طلب احد الاشخاص شراء 100 عضو الى كروب 🔝 •
- رابط الكروب ↙️ •
$text",
]);
}
if($data == "ch100" and $get >= 400){
file_put_contents("$from_id.txt", "ch100");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل رابط قناتك او معرف لا غير ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "ch100" and $get <= 400){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"w"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "ch100"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 400 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 400;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء 100 عضو الى قناة 🔝 •
- رابط القناة او معرف ↙️ •
$text",
]);
bot("sendmessage",[
"chat_id"=>$sud,
"text"=>"- طلب احد الاشخاص شراء 100 عضو الى قناة 🔝 •
- رابط القناة او معرف ↙️ •
$text",
]);
}
if($data == "ch200" and $get >= 800){
file_put_contents("$from_id.txt", "ch200");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل رابط قناتك او معرف لا غير ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "ch200" and $get <= 800){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"w"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "ch200"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 800 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 800;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء 200 عضو الى قناة 🔝 •
- رابط القناة او معرف ↙️ •
$text",
]);
bot("sendmessage",[
"chat_id"=>$sud,
"text"=>"- طلب احد الاشخاص شراء 200 عضو الى قناة 🔝 •
- رابط القناة او معرف ↙️ •
$text",
]);
}
if($data == "ch300" and $get >= 1200){
file_put_contents("$from_id.txt", "ch300");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل رابط قناتك او معرف لا غير ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "ch300" and $get <= 1200){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"w"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "ch300"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 1200 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 1200;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء 300 عضو الى قناة 🔝 •
- رابط القناة او معرف ↙️ •
$text",
]);
bot("sendmessage",[
"chat_id"=>$sud,
"text"=>"- طلب احد الاشخاص شراء 300 عضو الى قناة 🔝 •
- رابط القناة او معرف ↙️ •
$text",
]);
}
if($data == "ch400" and $get >= 1600){
file_put_contents("$from_id.txt", "ch400");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل رابط قناتك او معرف لا غير ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "ch400" and $get <= 1600){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"w"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "ch400"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 1600 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 1600;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء 400 عضو الى قناة 🔝 •
- رابط القناة او معرف ↙️ •
$text",
]);
bot("sendmessage",[
"chat_id"=>$sud,
"text"=>"- طلب احد الاشخاص شراء 400 عضو الى قناة 🔝 •
- رابط القناة او معرف ↙️ •
$text",
]);
}
if($data == "ch500" and $get >= 2000){
file_put_contents("$from_id.txt", "ch500");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل رابط قناتك او معرف لا غير ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "ch500" and $get <= 2000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"w"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "ch500"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 2000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 2000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء 500 عضو الى قناة 🔝 •
- رابط القناة او معرف ↙️ •
$text",
]);
bot("sendmessage",[
"chat_id"=>$sud,
"text"=>"- طلب احد الاشخاص شراء 500 عضو الى قناة 🔝 •
- رابط القناة او معرف ↙️ •
$text",
]);
}
// قسم البوتات
if($data == "e"){
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"
- بوت تشكر انستا بـ1000 👁‍🗨 •

- بوت ملازم منهج الجديد بـ1000 👁‍🗨 •

- بوت تحويل صيغ مميز بـ2000 👁‍🗨 •

- بوت لعبة رياضيات بـ2000 👁‍🗨•

- بوت لعبة XO بـ2000 👁‍🗨 •

- بوت لعبة مريم بـ2500 👁‍🗨 •

- بوت نسبة الحب بـ2500 👁‍🗨 •

- بوت رفع برابط مباشر بـ3000 👁‍🗨 •

- بوت تحميل من github بـ3000 👁‍🗨 •

- بوت حماية TPMaxBot بـ3000 👁‍🗨 •

- بوت الانحراف بـ8000 👁‍🗨 •

- بوت مروش متطور بـ8000 👁‍🗨 •

- بوت صنع سايت متطور بـ10000 👁‍🗨 •

- بوت صنع تواصل متطور بـ15000 👁‍🗨 •

- بوت مدير القناة ماركداون شفاف بـ20000 👁‍🗨 •

- بوت لستة شفافة بـ25000 👁‍🗨 •
", 
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"تشكر انستا",'callback_data'=>"b1"],['text'=>"بوت ملازم",'callback_data'=>"b2"]],
[['text'=>"تحويل صيغ",'callback_data'=>"b3"],['text'=>"لعبة رياضيات",'callback_data'=>"b4"]],
[['text'=>"لعبة XO",'callback_data'=>"b5"],['text'=>"لعبة مريم",'callback_data'=>"b6"]],
[['text'=>"نسبة الحب",'callback_data'=>"b7"],['text'=>"رفع برابط مباشر",'callback_data'=>"b8"]],
[['text'=>"تحميل من github",'callback_data'=>"b9"],['text'=>"TPMaxBot",'callback_data'=>"b10"]],
[['text'=>"الانحراف",'callback_data'=>"b11"],['text'=>"مروش",'callback_data'=>"b12"]],
[['text'=>"صنع سايت",'callback_data'=>"b13"],['text'=>"صنع تواصل",'callback_data'=>"b14"]],
[['text'=>"مدير القناة",'callback_data'=>"b15"],['text'=>"لستة شفافة",'callback_data'=>"b16"]],
[['text'=>"رجوع",'callback_data'=>"🔙"]],
]])
]);
}
if($data == "b1" and $get >= 1000){
file_put_contents("$from_id.txt", "bq1000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل توكن البوت معة فاصل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "b1" and $get <= 1000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"e"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "bq1000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 1000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 1000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء بوت تشكر 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "b2" and $get >= 1000){
file_put_contents("$from_id.txt", "b1000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل توكن البوت معة فاصل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "b2" and $get <= 1000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"e"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "b1000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 1000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 1000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء بوت ملازم 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "b3" and $get >= 1000){
file_put_contents("$from_id.txt", "bm1000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل توكن البوت معة فاصل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "b3" and $get <= 1000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"e"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "bm1000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 1000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 1000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء بوت ملازم 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "b4" and $get >= 2000){
file_put_contents("$from_id.txt", "b2000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل توكن البوت معة فاصل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "b4" and $get <= 2000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"e"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "b2000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 2000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 2000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء بوت تحويل صيغ 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "b5" and $get >= 2000){
file_put_contents("$from_id.txt", "bs2000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل توكن البوت معة فاصل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "b5" and $get <= 2000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"e"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "bs2000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 2000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 2000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء بوت لعبة رياضيات 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "b6" and $get >= 2000){
file_put_contents("$from_id.txt", "bx2000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل توكن البوت معة فاصل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "b6" and $get <= 2000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"e"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "bx2000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 2000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 2000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء بوت لعبة xo 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "b7" and $get >= 2500){
file_put_contents("$from_id.txt", "bs2500");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل توكن البوت معة فاصل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "b7" and $get <= 2500){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"e"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "bs2500"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 2500 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 2500;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء بوت نسبة الحب 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "b8" and $get >= 3000){
file_put_contents("$from_id.txt", "b3000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل توكن البوت معة فاصل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "b8" and $get <= 3000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"e"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "b3000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 3000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 3000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء بوت رفع برابط مباشر 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "b9" and $get >= 3000){
file_put_contents("$from_id.txt", "ba3000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل توكن البوت معة فاصل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "b9" and $get <= 3000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"e"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "ba3000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 3000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 3000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء بوت تحميل من جيت هاب 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "b10" and $get >= 3000){
file_put_contents("$from_id.txt", "bl3000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل توكن البوت معة فاصل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "b10" and $get <= 3000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"e"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "bl3000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 3000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 3000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء بوت TPMaxBot 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "b11" and $get >= 8000){
file_put_contents("$from_id.txt", "b8000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل توكن البوت معة فاصل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "b11" and $get <= 8000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"e"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "b8000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 8000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 8000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء بوت الانحراف 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "b12" and $get >= 8000){
file_put_contents("$from_id.txt", "b08000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل توكن البوت معة فاصل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "b12" and $get <= 8000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"e"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "b08000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 8000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 8000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء بوت مروش 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "b13" and $get >= 10000){
file_put_contents("$from_id.txt", "b10000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل توكن البوت معة فاصل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "b13" and $get <= 10000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"e"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "b10000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 10000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 10000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء بوت صنع سايت 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "b14" and $get >= 15000){
file_put_contents("$from_id.txt", "b15000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل توكن البوت معة فاصل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "b14" and $get <= 15000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"e"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "b15000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 15000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 15000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء بوت صنع تواصل 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "b15" and $get >= 20000){
file_put_contents("$from_id.txt", "b20000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل توكن البوت معة فاصل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "b15" and $get <= 20000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"e"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "b20000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 20000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 20000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء بوت ادارة قناة 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "b16" and $get >= 25000){
file_put_contents("$from_id.txt", "b25000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل توكن البوت معة فاصل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "b16" and $get <= 25000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"e"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "b25000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 25000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 25000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء بوت لسته شفافه 🔝 •
- معلوماته ↙️ •
$text",
]);
}
// قسم الحسابات
if($data == "r"){
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"
- حساب سوق بلي امركي بـ3000 👁‍🗨 •

- حساب سوق بلي عادي بـ1500 👁‍🗨 •

- حساب فيس روسي بـ2000 👁‍🗨 •

- حساب فيس عادي بـ1500 👁‍🗨 •
", 
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"سوق بلي امريكي",'callback_data'=>"l1"],['text'=>"سوق بلي عادي",'callback_data'=>"l2"]],
[['text'=>"فيس روسي",'callback_data'=>"l3"],['text'=>"فيس عادي",'callback_data'=>"l4"]],
[['text'=>"رجوع",'callback_data'=>"🔙"]],
]])
]);
}
if($data == "l1" and $get >= 3000){
file_put_contents("$from_id.txt", "l3000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "l1" and $get <= 3000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"r"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "l3000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 3000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 3000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء حساب سوق بلي امريكي 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "l2" and $get >= 1500){
file_put_contents("$from_id.txt", "l1500");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "l2" and $get <= 1500){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"r"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "l1500"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 1500 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 1500;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء حساب سوق بلي عادي 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "l3" and $get >= 2000){
file_put_contents("$from_id.txt", "l2000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "l3" and $get <= 2000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"r"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "l2000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 2000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 2000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء حساب فيس روسي 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "l4" and $get >= 1500){
file_put_contents("$from_id.txt", "ls1500");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل معرفك ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "l4" and $get <= 1500){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"r"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "ls1500"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 1500 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 1500;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء حساب فيس عادي 🔝 •
- معلوماته ↙️ •
$text",
]);
}
// قسم يوزرات vps
if($data == "t"){
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"
- يوزر شهري + بوت كامل بـ8000 🛡 •

- يوزر شهري بـ5000 🛡 •
", 
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"يوزر",'callback_data'=>"i1"],['text'=>"بوت كامل",'callback_data'=>"i2"]],
[['text'=>"رجوع",'callback_data'=>"🔙"]],
]])
]);
}
if($data == "i2" and $get >= 8000){
file_put_contents("$from_id.txt", "t8000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل معرفك فاصله توكن ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "i2" and $get <= 8000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"r"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "t8000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 8000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 8000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء بوت vps 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "i1" and $get >= 5000){
file_put_contents("$from_id.txt", "t5000");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- ارسل معرفك فاصله توكن ☑️ •", 
'message_id'=>$message_id, 
]);
}
if($data == "i1" and $get <= 5000){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- عذرا رصيدك غير كافي ❌ •",
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"شراء نقاط",'callback_data'=>"stor"]],
[['text'=>"رجوع",'callback_data'=>"r"]],
]])
]);
}
if($text and file_get_contents("$from_id.txt") == "t5000"){
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم خصم 5000 نقطه من حسابك ☑️ •",
"reply_to_message_id"=>$message_id,
]);
$k = file_get_contents("data/$from_id.txt");
$yes = $k - 5000;
file_put_contents("data/$from_id.txt", $yes);
unlink("$from_id.txt");
bot("sendmessage",[
"chat_id"=>$sudo,
"text"=>"- طلب احد الاشخاص شراء بوت vps 🔝 •
- معلوماته ↙️ •
$text",
]);
}
if($data == "stor"){
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"
- اسعار نقاط بـ$ 📲 •
- كرتات اسيا فقط 🔋 •
$5 = 5000 
$10 = 11000
$15 = 17000
$20 = 23000
$25 = 30000 
- للشراء راسل المطور ☑️ •
", 
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"المطور",'url'=>"https://t.me/$sudobot"]],
[['text'=>"رجوع",'callback_data'=>"🔙"]],
]])
]);
}
}
//___________________________________________________________________
if(preg_match('/^\/(add) (.*)/', $text, $add) and $from_id == $sudo or $from_id == $sud){
file_put_contents("ch.txt", $add[2]);
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"- تم اضافة القناة ($add[2]) في الدعم 📊 •",
]);
}
if(preg_match('/^\/(set) (.*) (.*)/', $text, $set) and $from_id == $sudo){
$k = file_get_contents("data/$set[2].txt");
$yes = $k + $set[3];
file_put_contents("data/$set[2].txt", $yes);
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"
- تم اضافة رصيد للعضو ( $set[2] ) 🎩 •
- فئة التعبئة :: $set[3] 📊 •
",
]);
bot("sendmessage",[
"chat_id"=>$set[2],
"text"=>"- تم اضافة رصيد ($set[3]) ع حسابك اصبح :: $yes 📊 •",
]);
}
if(preg_match('/^\/(del) (.*) (.*)/', $text, $set) and $from_id == $sudo){
$k = file_get_contents("data/$set[2].txt");
$yes = $k - $set[3];
file_put_contents("data/$set[2].txt", $yes);
bot("sendmessage",[
"chat_id"=>$chat_id,
"text"=>"
- تم سحب ($set[3]) نقطة بنجاح 👁‍🗨 •
- من العضو ($set[2]) 🚫 •
",
]);
bot("sendmessage",[
"chat_id"=>$set[2],
"text"=>"- قد سحب مطور البوت منك ($set[3]) بسبب مخالفة 🤷‍♂ •",
]);
}
if($data == "back"){
unlink("unll.txt");
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"*Welcome* _to the orders of_ *Admins* ❤\n*/add [user]* _Add channel support to_\n*/set [id]* _Add Balance to user_\n*/del [id]* _Delete Balance to user_", 
'parse_mode'=>markdown, 
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"broadcast forward ?",'callback_data'=>"bcfwd"],['text'=>"broadcast ?",'callback_data'=>"bc"]],
[['text'=>"Users ?",'callback_data'=>"users"]],
]])
]);
}
if($text == "/admin" and $chat_id == $sudo){ 
bot('sendMessage',[
'chat_id'=>$chat_id, 
'text'=>"*Welcome* _to the orders of_ *Admins* ❤\n*/add [user]* _Add channel support to_\n*/set [id]* _Add Balance to user_\n*/del [id]* _Delete Balance to user_", 
'parse_mode'=>markdown, 
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"broadcast forward ?",'callback_data'=>"bcfwd"],['text'=>"broadcast ?",'callback_data'=>"bc"]],
[['text'=>"Users ?",'callback_data'=>"users"]],
]])
]);
}
if($data == "users"){ 
$user = count($users); 
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"🔰┊_Users_ >*$user*", 
'message_id'=>$message_id, 
'parse_mode'=>markdown, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"🔙",'callback_data'=>"back"]],
]])
]);
}
if($data == "bcfwd"){ 
file_put_contents("unll.txt", "fwd"); 
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- Send the message to be shared 🔄 •", 
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"🔙",'callback_data'=>"back"]],
]])
]);
}
if($text and !$data and file_get_contents("unll.txt") == "fwd" and $chat_id == $sudo){ 
for($h=0;$h<count($users);$h++){ 
file_put_contents("unll.txt", "unll"); 
bot('forwardMessage',[ 
'chat_id'=>$users[$h], 
'from_chat_id'=>$chat_id, 
'message_id'=>$message_id,
]); 
}}
if($data == "bc"){ 
file_put_contents("unll.txt", "bc"); 
bot('editmessagetext',[ 
'chat_id'=>$chat_id, 
'text'=>"- Send the message to be shared 🔄 •", 
'message_id'=>$message_id, 
'reply_markup'=>json_encode([ 
'inline_keyboard'=>[
[['text'=>"🔙",'callback_data'=>"back"]],
]])
]);
}
if($text and !$data and file_get_contents("unll.txt") == "bc" and $chat_id == $sudo){ 
for($h=0;$h<count($users);$h++){ 
file_put_contents("unll.txt", "unll"); 
bot('sendMessage',[ 
'chat_id'=>$users[$h], 
'text'=>$text, 
'parse_mode'=>markdown, 
'disable_web_page_preview'=>true,
]); 
}}
?>

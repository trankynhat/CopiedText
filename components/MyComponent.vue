<template>
    <div>
        <div style="display: flex;">
            <img src="./wcare.png" width="150px" object-fit = cover>
            <h1 style="">Chào bạn</h1>
        </div>
        <div>
            <div style=" display: flex; justify-content: center;">
                <input type="text" placeholder="Enter your text" id="username">
                <button @click="copyToClipboard" style="margin: 10px;">Copy</button>
            </div>
            <div v-if="showNotification" class="notification"
                style="display: flex;align-items: center; position: fixed; bottom: 20px; left: 0; width: 100%; background-color: #f0f0f0;">
                <div style="width: 80%;text-align: center;margin-left: 10%;">{{ output_text }}</div>
                <button @click="closeNotification">Close</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'IndexPage',
    data() {
        return {
            showNotification: false
        };
        return {

        };
    },
    methods: {
        setContent(content) {
            this.output_text = content;
        },
        closeNotification() {
            this.showNotification = false;
        },
        copyToClipboard() {
            // Lấy tham chiếu đến phần tử với id "myInput"
            const inputElement = document.getElementById("username");
            // Lấy nội dung từ phần tử
            const content = inputElement.value;
            if (inputElement && content != "") {


                // Tạo một thẻ textarea ẩn để chứa nội dung cần sao chép
                const textarea = document.createElement("textarea");
                textarea.value = content;
                document.body.appendChild(textarea);

                // Chọn toàn bộ nội dung trong textarea
                textarea.select();

                try {
                    // Thực hiện lệnh sao chép
                    document.execCommand("copy");
                    this.setContent("Copied!");
                } catch (err) {
                    this.setContent("Can't copy!");
                }

                // Xóa textarea khỏi DOM
                document.body.removeChild(textarea);
            } else {
                this.setContent("Your text is empty!");
            }
            this.showNotification = true
        }
    }
}

</script>


<style>
.centered-box {
    text-align: center;
    background-color: #64676a;

}

.notification {
    padding: 10px;
    background-color: #f0f0f0;
    border: 1px solid #ccc;
    border-radius: 4px;
    margin-top: 10px;
}

h1 {
    font-size: 24px;
}

input[type="text"] {
    padding: 10px;
    margin: 10px;
    width: 200px;
}

button {
    padding: 10px;
    background-color: #3f4347;
    color: #fff;
    border: none;
    cursor: pointer;
}
</style>
<template>
    <div class="ths_imgUpload">
        <div class="th_imgUpload-icon"
            v-html="iconUnicode">
        </div>
        <div class="th_imgUpload-placeholder"
            v-if="placeholder"
            v-text="placeholder">
        </div>
        <div class="th_imgUpload-previewBox">
            <img :src="dataUrl" alt="" />
        </div>
        <label class="th_imgUpload-label"
            :for="readonly ? '' : myInputId"></label>
        <input class="th_imgUpload-input"
            :type="type"
            :id="myInputId"
             />
    </div>
</template>

<script>
import { IMG_TYPE, THEME_TYPE,
    IMG_TYPE_MAP } from '../constants';

export default {
    name: 't-img-upload',
    props: {
        imgUrl: { // 图片的url地址
            type: String
        },
        icon: { // 图片类型（默认是图片）
            type: String,
            default: IMG_TYPE.IMG
        },
        placeholder: { // 描述文案
            type: String,
            default: '点击或拖拽选择图片'
        },
        theme: { // 主题（默认是light主题）
            type: String,
            default: THEME_TYPE.LIGHT
        },
        aliIcon: { // 图片的unicode码
            type: String
        },
        readonly: { // 是否只读
            type: Boolean,
            default: false
        },
        inputId: { // input的id
            type: String
        },
        type: { // input类型
            type: String,
            default: 'file'
        },
        accept: { // input的accept值
            type: String,
            default: 'image/*,video/*'
        }
    },
    data () {
        const _that = this;
        return {
            dataUrl: _that.imgUrl || '',
            myInputId: _that.inputId || ''
        };
    },
    computed: {
        /**
         * 过滤图片类型
         * @returns {String} 返回图片类型
         */
        myIcon () {
            const _that = this;
            let res = '';

            if (_that.icon) {
                res = _that.icon;
            } else {
                res = _that.theme === THEME_TYPE.LIGHT ? IMG_TYPE.IMG : IMG_TYPE.CLIP;
            }
            return res;
        },
        /**
         * 过滤图片的unicode
         * @param {String} 返回图片的unicode码
         */
        iconUnicode () {
            return _that.aliIcon || IMG_TYPE_MAP[_that.myIcon];
        }
    }
}
</script>


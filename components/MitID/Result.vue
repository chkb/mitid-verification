<template>
  <div
    class="relative transform overflow-hidden place-content-center rounded-lg bg-white shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg"
  >
    <div class="self-center p-4">
      <div class="mitid-core-finalize">
        <div class="mitid-core-finalize__logo">
          <img src="/mitid.png" width="50" alt="" />
        </div>
        <div
          class="mitid-core-finalize__state"
          role="alertdialog"
          aria-busy="true"
          aria-live="assertive"
        >
          <div
            focusable="false"
            aria-hidden="true"
            class="mitid-core-finalize__shield"
          >
            <svg version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg">
              <path
                d="M49.9,0l50,15v41.2c0,47.8-50,60.8-50,60.8s-50-13-50-60.8V15L49.9,0"
              />
            </svg>
          </div>
          <div className="mitid-core-finalize__done"></div>
        </div>
        <h1 class="mitid-core-finalize__title">Verified</h1>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
.mitid-core-finalize {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  flex-direction: column;
  flex: 1 1 auto;

  &__logo {
    height: 24px;
    position: relative;
    width: 62px;
    margin-bottom: 24px;
    &-svg {
      position: absolute;
      left: -85px;
      top: -20px;
      height: 62px;
      width: 234px;
      transform: scale(0.26);
      path {
        fill: blue;
      }
    }
  }

  &__shield {
    position: absolute;
    width: 100px;
    height: 117px;
    path {
      fill: blue;
    }
  }

  &__state {
    position: relative;
    margin-bottom: 24px;
    height: 120px;
    width: 100px;
    display: block;
  }

  &__title {
    font-size: 1.25rem;
    font-weight: font-weight(bold);
    line-height: 1.75rem;
    display: block;
    text-align: center;
    height: 60px;
  }

  &__done:after {
    opacity: 0;
    height: 34px;
    width: 14px;
    transform-origin: left top;
    border-right: 4px solid #fff;
    border-top: 4px solid #fff;
    content: '';
    left: 32px;
    top: 55px;
    position: absolute;
    animation-duration: 800ms;
    animation-delay: 100ms;
    animation-timing-function: ease-in;
    animation-name: checkmark;
    animation-fill-mode: forwards;
    transform: scaleX(-1) rotate(135deg);
  }
}

@keyframes checkmark {
  0% {
    height: 0;
    width: 0;
    opacity: 1;
  }
  20% {
    height: 0;
    width: 14px;
    opacity: 1;
  }
  35% {
    height: 34px;
    width: 14px;
    opacity: 1;
  }
  100% {
    height: 34px;
    width: 14px;
    opacity: 1;
  }
}
</style>

<template>
<f7-page name="signin">
    <f7-navbar back-link="Back" title="Add fuel fill"></f7-navbar>

    <div class="card">
        <div class="card-header">Add fuel fill</div>
        <div class="card-content">

            <div class="list">
                <ul>

                    <li class="item-content item-input">
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Km. óra állása</div>
                            <div class="item-input-wrap">
                                <input type="number" name="autoKm" autofocus="autofocus" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    <!--/li>
                    <li class="item-content item-input"-->
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Megtett Km.</div>
                            <div class="item-input-wrap">
                                <input type="number" name="autoUsedFuel" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    </li>
					
                    <li class="item-content item-input">
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Fogy. üzema.</div>
                            <div class="item-input-wrap">
                                <input type="number" name="autoUsedFuel" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    <!--/li>
                    <li class="item-content item-input"-->
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Átlagos fogy.</div>
                            <div class="item-input-wrap">
                                <input type="number" name="autoUsedFuel" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    </li>
					

                    <li class="item-content item-input">
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Benzínkút</div>
                            <div class="item-input-wrap">
                                <input type="number" name="autoUsedFuel" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    </li>
                    <li class="item-content item-input">
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Üzemanyag típusa</div>
                            <div class="item-input-wrap">
                                <input type="text" name="filledType" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    <!--/li>
                    <li class="item-content item-input"-->
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Tankolt liter</div>
                            <div class="item-input-wrap">
                                <input type="number" name="autoUsedFuel" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    </li>
                    <li class="item-content item-input">
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Egységár</div>
                            <div class="item-input-wrap">
                                <input type="number" name="autoUsedFuel" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    <!--/li>
                    <li class="item-content item-input"-->
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Kedv.egys.ár</div>
                            <div class="item-input-wrap">
                                <input type="number" name="autoUsedFuel" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    </li>
                    <li class="item-content item-input">
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Fizettendő</div>
                            <div class="item-input-wrap">
                                <input type="number" name="autoUsedFuel" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    <!--/li>
                    <li class="item-content item-input"-->
                        <div class="item-inner">
                            <div class="item-title item-floating-label">Kedv.végösszeg</div>
                            <div class="item-input-wrap">
                                <input type="number" name="autoUsedFuel" />
                                <span class="input-clear-button"></span>
                            </div>
                        </div>
                    </li>

                </ul>
            </div>

        </div>
        <div class="card-footer justify-content-center" style="padding-top: 30px;">
            <f7-button class="col color-deeppurple" fill raised>Mentés</f7-button>
        </div>
    </div>

	<br v-for="i in 10">

</f7-page>
</template>

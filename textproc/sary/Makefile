PORTNAME=	sary
PORTVERSION=	1.2.0
PORTREVISION=	6
CATEGORIES=	textproc
MASTER_SITES=	http://sary.sourceforge.net/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Suffix array library and tools, which provide fast full-text search
WWW=		https://sary.sourceforge.net/index.html.en

DEPRECATED=	Last release in 2005 and unmaintained in tree for years
EXPIRATION_DATE=2025-04-30

USES=		gnome libtool pathfix pkgconfig
USE_GNOME=	glib20
USE_LDCONFIG=	yes

GNU_CONFIGURE=	yes
GNU_CONFIGURE_MANPREFIX=${PREFIX}/share

OPTIONS_DEFINE=	DOCS

.include <bsd.port.options.mk>

.if ${OPSYS} == FreeBSD
CFLAGS+=	-Wno-error=incompatible-function-pointer-types
.endif

post-patch:
	@${REINPLACE_CMD} -e '/^SUBDIRS/s|docs||g' ${WRKSRC}/Makefile.in

post-install:
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/libsary.so

post-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	cd ${WRKSRC}/docs && ${FIND} . ! -name "*Makefile*" | \
		${CPIO} -pdm -L -R ${SHAREOWN}:${SHAREGRP} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
